# Engenharia de Resiliência e Disaster Recovery (RCA)

## 1. Visão Executiva e Governança de Dados

A garantia de Alta Disponibilidade (HA) não reside apenas na replicação contínua, mas na capacidade de mitigação e recuperação rápida perante cenários de falha catastrófica. 

Este documento detalha os **Procedimentos Operacionais Padrão (SOP)** e arquiteturas de *troubleshooting* aplicadas para garantir a resiliência dos motores de bases de dados relacionais (MySQL Percona e SQL Server) em ambientes de missão crítica.

---

## 2. Tuning de SO e Prevenção de Gargalos (OOM Killer)

Para suportar ambientes com alta concorrência e milhares de conexões simultâneas, a configuração padrão do sistema operativo (Linux) e do Systemd gera frequentemente gargalos de *File Descriptors* e intervenções agressivas do *OOM (Out of Memory) Killer*.

### ⚙️ Configuração de Limites (Systemd Override)
A parametrização abaixo é injetada na inicialização do serviço MySQL (`override.conf`) para isolar o motor de dados das políticas de encerramento do *kernel* Linux em caso de *stress* de memória, garantindo estabilidade no processamento:

```ini
[Service]
ExecStartPre=-/usr/bin/touch /var/log/log-slow-queries.log
ExecStartPre=-/usr/bin/chown mysql:mysql /var/log/log-slow-queries.log
LimitNOFILE=130000
LimitNPROC=130000
LimitMEMLOCK=130000
OOMScoreAdjust=-1000  # Protege o processo do OOM Killer
```

### 📂 Isolamento de Storage (I/O)
Para evitar que o crescimento da base de dados comprometa a partição raiz (`/var/lib`), o diretório de dados é migrado para um ponto de montagem dedicado (ex: `/dbdir`), otimizando o *throughput* de I/O:

```bash
# Paragem controlada dos serviços de aplicação e motor
sudo systemctl stop mysqld

# Migração física e criação de link simbólico para transparência da aplicação
sudo mv /var/lib/mysql /dbdir/
sudo ln -s /dbdir/mysql /var/lib/
```

---

## 3. Disaster Recovery (DR): Recuperação de Crashes

Em cenários de corrupção de *tablespaces* (ex: falhas de hardware ou *crashes* abruptos do *daemon*), o processo de *Root Cause Analysis* (RCA) dita o plano de ação adequado.

### 🛡️ Recovery Estrutural (Sem Backup Válido)
Quando o binlog ou os ficheiros `.ibd` são irrecuperavelmente corrompidos, utiliza-se a técnica de reconstrução estrutural isolando chaves e forçando a integridade referencial:

1. **Isolamento:** *Backup* físico a frio do diretório corrompido (`cp -R -p /dbdir/mysql /dbdir/mysql_crash`).
2. **Reconstrução:** *Drop* da base afetada e recriação da estrutura (DDL) a partir dos ficheiros de *dump* nativos.
3. **Injeção de Dados (Sanitizada):** Importação dos dados com tratamento de conflitos (`INSERT IGNORE`) via `sed` para evitar interrupções por chaves duplicadas.
4. **Sincronização de Motores Alternativos:** Uso de `rsync` paramétrico para migrar ficheiros físicos MyISAM (ignorando metadados corrompidos como `.frm` ou `.ibd` do InnoDB).

---

## 4. Capacity Planning: Migração de Storage (SQL Server)

Como parte do plano de capacidade, é frequente a necessidade de migrar ficheiros físicos (MDF/LDF) de bases de dados massivas no **SQL Server** para *storages* mais rápidos (NVMe) ou de maior volume, minimizando o *downtime*.

O procedimento arquitetado evita a necessidade morosa de *Backup & Restore*, alterando os apontamentos lógicos no *Master* e movendo os blocos físicos com a base momentaneamente em estado `OFFLINE`:

```sql
-- 1. Modificação do Apontamento Lógico nos Metadados
ALTER DATABASE [NomeDoBanco]
MODIFY FILE (NAME = 'NomeLogicoDoMDF', FILENAME = 'E:\SQLServer\Data\NomeDoBanco.mdf');

-- 2. Congelamento Transacional (Isolamento)
ALTER DATABASE [NomeDoBanco] SET OFFLINE WITH ROLLBACK IMMEDIATE;
```
*(Durante este lapso de segundos/minutos, os ficheiros físicos são migrados via PowerShell para a nova LUN preservando o ACL do serviço `NT SERVICE\MSSQLSERVER`).*

```sql
-- 3. Reativação e Auditoria de Integridade
ALTER DATABASE [NomeDoBanco] SET ONLINE;
DBCC CHECKDB('NomeDoBanco') WITH NO_INFOMSGS;
```

---

## 5. Ciclo de Vida de Dados: Transição para "Cold Data"

Para evitar a degradação de *performance* em bases de dados transacionais, nós operamos a transição de instâncias de produção para instâncias de "Histórico" (*Read-Only*). 

Este processo envolve:
* **Segmentação de Carga:** O tráfego transacional primário é desviado para o novo *cluster*.
* **Adequação de Recursos:** O *tuning* do `my.cnf` do nó legado é ajustado para privilegiar leituras analíticas pesadas (relatórios) em vez de escritas.
* **Desativação de Agentes:** Serviços paralelos (*Daemons* de integração) são desligados no nó legado para poupar processamento.

