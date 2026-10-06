# Portal de Observabilidade DBA + IA

O monitoramento tradicional avisa quando o banco de dados caiu; a observabilidade moderna explica o porquê e como evitar que aconteça novamente. O **Portal de Observabilidade DBA + IA** nasceu da necessidade de centralizar indicadores operacionais, cruzar métricas de infraestrutura e acelerar a resposta a incidentes (RCA) em ambientes críticos[cite: 2, 3].

---

## 🎯 O Desafio da Sustentação de Dados

Em operações complexas suportadas por múltiplos servidores **MySQL Percona** e **SQL Server**, a investigação de um gargalo de performance frequentemente exige que o DBA acesse diversas ferramentas desconexas (logs do Linux, painéis de rede, Zabbix, *slow query logs*)[cite: 2, 3]. O desafio era eliminar essa fragmentação, construindo uma plataforma única que não apenas mostrasse o estado atual, mas entregasse os recursos de diagnóstico mastigados para a equipe técnica.

## 🛠️ Arquitetura e Engenharia End-to-End

Atuei no desenvolvimento de ponta a ponta desta solução, aplicando engenharia de software para resolver um problema de infraestrutura de dados[cite: 3]:

* **Backend e APIs:** Desenvolvimento do motor da aplicação utilizando **Python** e **FastAPI**, responsável por consumir dados estruturados dos servidores e consolidar logs pesados em frações de segundo[cite: 2, 3].
* **Frontend e Visualização:** Estruturação de interfaces responsivas utilizando **JavaScript e CSS** para garantir uma navegação fluida, operando em sinergia com o **Grafana** para a renderização de gráficos e séries temporais[cite: 2, 3].
* **Integração com IA e Diagnóstico:** Implementação de recursos focados em extrair padrões de falha (*Root Cause Analysis* - RCA), destacando *queries* ofensoras, contenção de *locks* e anomalias no consumo de hardware antes que derrubem a operação[cite: 2, 3].

## 🔍 Funcionalidades Principais

1. **Visão Holística do Ambiente:** Centralização de indicadores de saúde dos clusters de banco de dados (CPU, I/O, conexões ativas e *replication lag*) em um único painel de controle[cite: 2].
2. **Troubleshooting Acelerado:** Ferramentas integradas para investigar desvios de comportamento em tempo real, permitindo aos times de suporte e DBA identificar a origem de um problema de lentidão sem precisar garimpar logs via terminal[cite: 2, 3].
3. **Métricas de Negócio x Infraestrutura:** Conexão do impacto técnico (como uma tabela *lockada*) com o processo de negócio afetado, melhorando a comunicação do status da operação.

## 📊 Impacto Operacional

* **Redução do MTTR (Mean Time to Recovery):** A centralização de informações e o uso de recursos de diagnóstico reduziram drasticamente o tempo necessário para identificar e mitigar *crashes* em produção[cite: 2, 3].
* **Autonomia Sistêmica:** Transformação de dados brutos de telemetria em *insights* acionáveis, permitindo que a gestão tome decisões antecipadas de *tuning* ou expansão de infraestrutura.
* **Escalabilidade:** A arquitetura baseada em APIs REST (FastAPI) garante que novos servidores ou bancos de dados possam ser "plugados" à plataforma de observabilidade com o mínimo de atrito[cite: 2, 3].

---

> *"Automação sem observabilidade vira caixa-preta. Observabilidade sem ação vira dashboard. O objetivo desta arquitetura é conectar dados e infraestrutura para que a equipe possa detectar, entender e agir."*[cite: 2]
