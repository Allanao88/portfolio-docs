# Resiliência e Root Cause Analysis (RCA)

## 1. Visão Executiva (Redução de Toil)

Na engenharia de confiabilidade (SRE/DBA), a automação é a principal ferramenta para reduzir o *toil* (trabalho manual, repetitivo e sem valor arquitetural) e mitigar o erro humano. 

Este repositório documenta os principais *scripts* e rotinas automatizadas em Bash e Python utilizados para gestão de estado, *backups* lógicos a quente e sincronização de topologia nos *clusters* de bases de dados relacionais.

---

## 2. Backup Lógico Otimizado (Hot Backup)

Em ambientes 24/7 com alta concorrência transacional, os *backups* lógicos não podem causar bloqueios de tabela (*Table Locks*). O *script* abaixo é utilizado para extrair dados massivos (ex: histórico de tabelas core) garantindo a consistência através de *snapshots* transacionais.

### 📦 Exportação com Compressão On-The-Fly
```bash
# Execução do dump garantindo consistência transacional sem lock de leitura/escrita
sudo mysqldump asteriskcdrdb chamadas_backup \
  --quick \
  --single-transaction \
  --skip-extended-insert \
  --complete-insert \
  --insert-ignore \
  --no-create-info \
  --skip-add-locks | sudo gzip > /storage/bkp/chamadas_backup_$(date +%F).sql.gz
```
* **Engenharia aplicada:** O encadeamento (`| gzip`) evita que o *dump* não comprimido consuma excessivamente o I/O do disco local, transferindo a carga para a CPU e gravando diretamente o binário comprimido.

---

## 3. Configuration Management (Sincronização de Cluster)

Para garantir que os nós de um *cluster* (Master/Replicas) operem com a exata mesma parametrização, os ficheiros de configuração (`my.cnf`) devem ser geridos como código ou sincronizados ativamente.

### 🔄 Espelhamento de Configuração Paramétrica
Em vez de edição manual em múltiplos nós, a rotina de sincronização sobre SSH garante a paridade do *tuning*:
```bash
#!/bin/bash
# Sincronização do ficheiro de tuning (my.cnf) do Master primário para as instâncias B2 e M1
DESTINOS=("10.0.0.12" "10.0.0.13")

for IP in "${DESTINOS[@]}"; do
  echo "Sincronizando my.cnf para $IP..."
  sudo rsync -avz /etc/my.cnf root@$IP:/etc/ --progress
done
# Após a execução, um handler reinicia o serviço nos nós de destino
```

---

## 4. Sincronização Física de Dados a Frio

Durante processos de *Disaster Recovery* ou clonagem de ambientes massivos, a migração lógica é demasiado lenta. Nestes casos, acionamos *scripts* de transferência física de blocos, filtrando estritamente as extensões permitidas.

### 🚀 Clonagem Incremental de Ficheiros Físicos
```bash
#!/bin/bash
# Sincronização de blocos físicos, ignorando metadados e motores corrompidos
DIR_ORIGEM="/dbdir/mysql_crash_20240909/asteriskcdrdb/"
DIR_DESTINO="/dbdir/mysql/asteriskcdrdb/"

sudo rsync -avn $DIR_ORIGEM $DIR_DESTINO \
  --exclude="*.frm" \
  --exclude="*.ibd" \
  --exclude="*.TRG" \
  --exclude="*.TRN" \
  --exclude="*.par" \
  --exclude="*.opt" \
  --progress
```
* **Engenharia aplicada:** O uso da flag `-n` (*dry-run*) na primeira execução atua como uma validação de segurança antes da efetivação (`-v` verbose). A exclusão estrita (`--exclude`) garante que os *tablespaces* não sofram corrupção cruzada durante o *recovery*.

---

## 5. Integração e Gatilhos de Aplicação

A administração de bases de dados em ecossistemas de alta criticidade não ocorre num vácuo. A resolução de um incidente no motor frequentemente requer o acionamento de gatilhos nas aplicações que consomem esses dados.

```bash
# Gatilhos acionados via terminal após sincronização de base para atualizar os dados de telecom
sudo /root/devbin/sync_anatel_prefixos <servidor_alvo>
sudo /var/lib/callflex/bin/emergencia
```
