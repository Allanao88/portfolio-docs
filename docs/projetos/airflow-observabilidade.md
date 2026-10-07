# Arquitetura Apache Airflow &amp; Automação Linux

Em ambientes corporativos de dados, a execução pontual de scripts isolados não é suficiente para garantir a confiabilidade de processos de negócio. A **Arquitetura de Orquestração com Apache Airflow e Automação Linux** foi projetada para transformar rotinas dispersas em um ecossistema modular, auditável, resiliente e altamente automatizado.

---

## 🎯 O Desafio de Orquestração

A sustentação de pipelines de dados frequentemente enfrenta falhas silenciosas, concorrência de recursos e dependências complexas entre sistemas. A solução adotada buscou eliminar execuções manuais ou agendamentos legados (como *cron jobs* sem visibilidade), substituindo-os por uma plataforma de orquestração programática containerizada, com controle de dependências e reexecução automática em caso de falha.

---

## 🛠️ Arquitetura e Engenharia de Pipelines

A arquitetura combina a flexibilidade do **Python** para lógica de negócios com a robustez do **Shell Script** para interação direta com o sistema operacional **Linux**:

* **DAGs Modulares em Python:** Construção de *Directed Acyclic Graphs* (DAGs) estruturadas de forma limpa e desacoplada, definindo explicitamente as dependências entre tarefas, agendamentos e regras de reexecução (*retries*).
* **Orquestração Híbrida (Python &amp; Shell Script):** Utilização do Airflow para gerenciar não apenas scripts nativos em Python, mas também *wrappers* e rotinas em **Shell Script (** **.sh** **)**, permitindo interagir diretamente com utilitários de sistema no Linux, realizar rotinas de transferência de arquivos, gerenciamento de permissões e execução de tarefas de infraestrutura.
* **Isolamento via Docker:** Implantação e execução de rotinas em ambientes isolados utilizando **Docker**, garantindo a padronização das dependências, facilidade de migração entre ambientes e sustentação de processos sem conflitos de versão.
* **Gestão de Variáveis &amp; Credenciais:** Parametrização segura de conexões a bancos de dados (**MySQL Percona**, **SQL Server**), chaves de APIs e variáveis de ambiente, prevenindo a exposição indevida de dados sensíveis no código.

---

## 🔍 Principais Funcionalidades

* **Tratamento de Exceções e Reexecução:** Configuração de regras automatizadas de *retries* com intervalos progressivos (*exponential backoff*), reduzindo a necessidade de intervenção humana em falhas temporárias de rede ou indisponibilidades momentâneas de SGBDs.
* **Rastreabilidade e Logs Centralizados:** Centralização de logs de execução para cada tarefa da DAG, acelerando a identificação da causa raiz em caso de interrupção do pipeline.
* **Notificações &amp; Alertas:** Integração de alertas para notificação imediata de falhas ou atrasos na execução de pipelines críticos de carga de dados.

---

## 📊 Impacto Operacional e de Negócio

* **Garantia de SLAs de Carga:** Estabilização dos horários de processamento e entrega de dados para relatórios gerenciais e sistemas analíticos.
* **Automação de Rotinas de Infraestrutura:** Eliminação de processos manuais de manutenção, extração e carga de dados, liberando tempo das equipes operacionais para tarefas estratégicas.
* **Observabilidade do Fluxo de Dados:** Visão clara do estado dos pipelines, histórico de execuções e tempo médio de conclusão de cada etapa do processo ETL/ELT.

---

&gt; **Princípio de Orquestração:** *"Se um pipeline precisa de intervenção manual para rodar diariamente, ele não é uma automação: é um débito técnico."*