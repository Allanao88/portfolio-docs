# Visão Geral de Projetos &amp; Cases Técnicos

Esta seção reúne o catálogo de projetos, arquiteturas e soluções implementadas nas frentes de **Engenharia de Dados**, **Administração de Bancos de Dados (DBA)**, **Automação de Infraestrutura** e **Governança Operacional**.

Cada case detalha os cenários técnicos encontrados, as decisões de arquitetura adotadas, as tecnologias empregadas e os resultados de negócio obtidos.

---

## 🚀 Engenharia de Dados, Observabilidade &amp; Automação

### 01 · [Portal de Observabilidade DBA + Monitorias DCI](portal-monitorizacao.md)

Plataforma unificada para centralização de métricas de saúde de bancos de dados, diagnósticos em tempo real e visualização operacional. Combina backend em **Python (FastAPI)**, interfaces web operacionais nativas em **HTML5 e CSS3** (`monitorias_dci/`) e painéis analíticos no **Grafana**.

* **Tecnologias:** `Python` · `FastAPI` · `HTML5 / CSS3` · `Grafana` · `MySQL`

### 02 · [Arquitetura Apache Airflow &amp; Automação Linux](airflow-observabilidade.md)

Ecossistema de orquestração programática de pipelines ETL/ELT e tarefas de infraestrutura. Utiliza DAGs modulares em **Python**, *wrappers* em **Shell Script (Bash)** para integração nativa com o Linux e execução containerizada com **Docker**.

* **Tecnologias:** `Apache Airflow` · `Docker` · `Python` · `Shell Script` · `ETL`

---

## 🗄️ Sustentação de Bancos de Dados (DBA) &amp; Resiliência

### 03 · [Resiliência, Troubleshooting &amp; RCA](../dba/resiliencia-rca.md)

Casos práticos de resolução de incidentes críticos, mitigação de *crashes*, eliminação de gargalos de I/O, otimização de consultas (*query tuning*) e aplicação de Análise de Causa Raiz em ambientes de produção com **MySQL Percona**, **SQL Server** e **Linux**.

* **Tecnologias:** `MySQL Percona` · `SQL Server` · `Linux` · `Query Tuning` · `RCA`

### 04 · [Scripts, Automações &amp; Sustentação de SGBDs](../dba/scripts.md)

Coletânea de rotinas automatizadas para manutenção preventiva, verificação de integridade, expurgo de dados e coleta de métricas em SGBDs. Estruturado com módulos em **Python**, scripts em **Shell Script** e conteinerização via **Dockerfile**.

* **Tecnologias:** `Python` · `Shell Script` · `Dockerfile` · `MySQL` · `SQL Server`

---

## ⚙️ Governança ITSM, Workflows &amp; CRM

### 05 · [GLPI 11 &amp; Governança ITSM](../crm/glpi.md)

Atuação como ponto focal técnico no projeto de modernização e migração da plataforma GLPI para a versão 11\. Envolveu preparação de infraestrutura Linux, otimização de banco de dados, estruturação de catálogo de serviços e transição com *zero downtime*.

* **Tecnologias:** `GLPI 11` · `ITSM` · `Linux` · `MySQL` · `SLA`

### 06 · [Bitrix24 &amp; Engenharia de Workflows](../crm/bitrix24.md)

Mapeamento de processos corporativos, automação de fluxos de trabalho (*business processes*) e integração do Bitrix24 via APIs REST em **Python** com bancos de dados relacionais e dashboards no **Power BI** e **Grafana**.

* **Tecnologias:** `Bitrix24` · `APIs REST` · `Python` · `Power BI` · `Workflows`

---

## 📌 Como Navegar pelos Cases

Utilize os links acima para explorar cada projeto individualmente e analisar as abordagens técnicas, decisões de arquitetura e impactos operacionais de cada solução.