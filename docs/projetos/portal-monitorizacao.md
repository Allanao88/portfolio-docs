# Portal de Observabilidade DBA + Monitorias DCI

O monitoramento tradicional apenas avisa quando um serviço cai; a observabilidade moderna explica o porquê e como evitar que volte a acontecer. O **Portal de Observabilidade DBA + Monitorias DCI** nasceu da necessidade de centralizar indicadores operacionais, cruzar métricas de infraestrutura de dados e fornecer interfaces nativas de diagnóstico para acelerar a resposta a incidentes.

---

## 🎯 O Desafio Operacional

Em ambientes complexos suportados por múltiplos servidores **MySQL Percona** e **SQL Server** em **Linux**, a investigação de um gargalo de desempenho frequentemente exige que a equipe acesse ferramentas desconexas (logs do sistema operacional, métricas de rede, Zabbix, *slow query logs*). O objetivo deste projeto foi eliminar a fragmentação de informações, construindo uma plataforma unificada que integre backend analítico e interfaces web operacionais customizadas.

---

## 🛠️ Arquitetura e Engenharia End-to-End

A solução foi construída unindo backend em Python, integrações via APIs REST, visualização de métricas e desenvolvimento de interfaces web operacionais nativas:

* **Backend &amp; Motores de Diagnóstico:** Desenvolvimento do ecossistema em **Python** (com **FastAPI**), responsável por consumir dados estruturados dos SGBDs, processar chamadas de API e consolidar logs operacionais em frações de segundo.
* **Interfaces Web Operacionais (Portal DCI):** Construção de páginas de monitoria responsivas e amigáveis utilizando **HTML5** e **CSS3** nativos (`monitorias_dci/`), garantindo acesso rápido e leve aos status de infraestrutura por equipes técnicas e operacionais.
* **Dashboards &amp; Séries Temporais:** Integração direta com o **Grafana** e **Streamlit** para renderização de gráficos em tempo real, tendências de consumo de hardware e acompanhamento de métricas de tráfego.
* **Diagnóstico Pró-ativo &amp; RCA:** Implementação de recursos focados em Análise de Causa Raiz (*Root Cause Analysis* \- RCA), destacando *queries* ofensoras, contenção de *locks* e anomalias de replicabilidade (*replication lag*) antes que afetem o usuário final.

---

## 🔍 Principais Funcionalidades

* **Visão Holística da Infraestrutura:** Centralização dos indicadores de saúde dos clusters de banco de dados (processamento, I/O de disco, conexões ativas e status de replicação) em um único portal web.
* **Troubleshooting Acelerado:** Painéis integrados para investigar desvios de comportamento em tempo real, permitindo a identificação imediata da origem de um problema de lentidão sem necessidade de garimpar logs via terminal.
* **Conexão entre Infraestrutura e Negócio:** Mapeamento do impacto técnico (como uma tabela temporariamente bloqueada) com o processo corporativo ou fila de atendimento afetada, garantindo visibilidade clara para gestores.

---

## 📊 Impacto Operacional e de Negócio

* **Redução do MTTR (** **Mean Time to Recovery** **):** A centralização de informações e o uso de telas operacionais dedicadas reduziram drasticamente o tempo necessário para identificar, diagnosticar e mitigar falhas em produção.
* **Autonomia para as Equipes:** Transformação de dados brutos de telemetria e logs complexos em visões visuais acionáveis, dando autonomia às equipes de suporte N2/N3 e DBA.
* **Arquitetura Escalável:** O modelo baseado em APIs REST em Python e interfaces web desconectadas permite acoplar novos servidores, bancos de dados ou módulos de monitoria com mínimo atrito.

---

&gt; **Princípio de Observabilidade:** *"Automação sem observabilidade vira caixa-preta. Observabilidade sem ação vira dashboard."*