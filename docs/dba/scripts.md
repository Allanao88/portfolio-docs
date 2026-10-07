# Scripts, Automações &amp; Sustentação de SGBDs

A administração eficiente de bancos de dados modernos exige a eliminação sistemática de tarefas manuais repetitivas. A página de **Scripts, Automações e Sustentação de SGBDs** reúne a documentação de rotinas desenvolvidas para automatizar a manutenção de infraestruturas **MySQL Percona** e **SQL Server**, garantir a segurança de credenciais e integrar bancos de dados a rotinas operacionais no **Linux**.

---

## 🎯 O Objetivo das Automações

Sistemas de bancos de dados em produção geram demandas diárias de manutenção, monitoramento de espaço, checagem de integridade e coleta de métricas. Executar essas atividades manualmente aumenta o risco de erro humano e consome tempo precioso da equipe. As automações foram desenvolvidas para funcionar de forma autônoma, auditável e resiliente em ambiente Linux.

---

## 🛠️ Arquitetura das Automações

A estrutura de automação é dividida em módulos especializados, utilizando as melhores práticas de desenvolvimento e infraestrutura:

* **Módulos em Python:** Desenvolvimento de rotinas em **Python** (`python/`) para conexão segura a SGBDs, manipulação de conjuntos de dados, consumo de APIs REST e execução de validações lógicas complexas.
* **Scripts de Infraestrutura em Shell (Bash):** Criação de rotinas em **Shell Script (** **.sh** **)** para execução direta no terminal Linux, cobrindo rotinas de backup, limpeza de arquivos temporários, monitoramento de uso de disco e chamadas de sistema.
* **Containerização com Dockerfile:** Padronização dos ambientes de execução de scripts através da criação de **Dockerfiles** dedicados, isolando bibliotecas e garantindo que os scripts rodem com o mesmo comportamento em qualquer servidor.
* **Conectividade Segura a SGBDs:** Implementação de drivers de conexão (*pooling* e conexões assíncronas) parametrizados para comunicação eficiente com instâncias **MySQL Percona** e **SQL Server**.

---

## 🔍 Principais Rotinas Desenvolvidas

* **Coleta de Métricas e Health Check:** Scripts programados para checar periodicamente o status das instâncias, espaço em disco, consumo de memória, tempo de execução de *queries* e estado das filas de replicação.
* **Integração via APIs REST:** Automação do envio de alertas e eventos operacionais para plataformas de comunicação ou sistemas de chamados (como Bitrix24 e GLPI), conectando eventos de banco de dados diretamente ao fluxo de trabalho da equipe.
* **Purga e Retenção Automatizada:** Rotinas seguras para expurgo de dados obsoletos, rotação de logs e manutenção de tabelas históricas, prevenindo o esgotamento de armazenamento no servidor.
* **Exportação e Processamento de Dados:** Scripts de extração e conversão automatizada de relatórios em múltiplos formatos para apoio a auditorias e rotinas operacionais.

---

## 🔒 Segurança e Boas Práticas

* **Gestão de Credenciais:** Supressão total de senhas ou chaves de acesso gravadas diretamente no código (*hardcoded*). Todas as credenciais são injetadas dinamicamente via variáveis de ambiente e cofres de segredos.
* **Tratamento de Exceções &amp; Logs:** Todos os scripts possuem blocos de tratamento de erros (`try/except` em Python e checagem de *exit status* em Shell), gravando logs estruturados para auditoria.
* **Execução Sem Impacto:** Rotinas de manutenção intensiva são projetadas para rodar com controle de concorrência ou em horários de menor tráfego, evitando contenção de recursos ou bloqueios em tabelas de produção.

---

## 📊 Impacto Operacional e de Negócio

* **Sustentação Preventiva:** Redução drástica de incidentes causados por falta de espaço em disco ou falhas não detectadas de replicação.
* **Padronização de Procedimentos:** Eliminação de variações operacionais entre membros da equipe, garantindo que as rotinas sigam exatamente o mesmo protocolo técnico.
* **Eficiência Operacional:** Liberação da equipe de DBA e infraestrutura de tarefas operacionais braçais, permitindo foco em otimização de performance (*tuning*) e arquitetura.

---

&gt; **Princípio de Automação:** *"Se uma tarefa precisa ser executada mais de duas vezes da mesma forma, ela deve ser transformada em código."*