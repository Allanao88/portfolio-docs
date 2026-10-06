# Portal de Observabilidade DBA + IA

> Case técnico existente do portfólio.

## Objetivo

Centralizar informações de operação, bancos, monitoramento e diagnóstico em uma interface única.

## Tecnologias

`Python` `FastAPI` `Grafana` `MySQL` `APIs`

## 1. Visão Executiva

O **Portal de Observabilidade de Engenharia de Dados** é uma solução corporativa de alta performance desenvolvida para centralizar a gestão de infraestrutura de bases de dados, orquestração de *pipelines* e métricas operacionais das equipas.

O grande diferencial arquitetural da plataforma é a integração nativa com um **Motor de Inteligência Artificial Local (LLM)**. Este ecossistema atua de forma autónoma no diagnóstico de falhas em *pipelines* de dados, reduzindo drasticamente o *Mean Time to Resolution* (MTTR) e transformando a postura da equipa de reativa para proativa.

---

## 2. Proposta de Valor e Funcionalidades Core

### 🧠 Diagnóstico Autônomo com IA (Observabilidade Inteligente)
*   **Análise de Root Cause em Tempo Real:** O sistema monitoriza continuamente o orquestrador de dados (Apache Airflow). Ao detetar uma falha (ex: DAG/Task interrompida), extrai os logs físicos e submete os *tracebacks* a um motor LLM operando em infraestrutura local.
*   **Zero Data-Leakage (Privacidade):** A utilização de IA local (modelo *Qwen2.5-Coder* conteinerizado) garante que nenhum dado sensível de infraestrutura ou log de erro é enviado para APIs externas na *cloud*.
*   **Leitura Imersiva para Engenheiros:** Interface otimizada com painéis laterais dinâmicos (*Offcanvas/Drawer*) que exibem as análises e *code blocks* gerados pela IA sem quebrar o layout da grelha de monitorização.

### 📊 Gestão de Infraestrutura e Governança de Dados
*   **Monitoria Multi-Motor:** Acompanhamento de indicadores de saúde, capacidade (disco, buffers, réplicas) e eventos anómalos em instâncias relacionais críticas (MySQL, SQL Server e PostgreSQL).
*   **Dashboards Executivos:** Painel central com gráficos interativos de eficiência operacional, distribuição de carga e saúde dos serviços em tempo real.

### 🛠️ Gestão de Incidentes e Produtividade Corporativa
*   **Integração ITSM Integrada:** Conexão fluida com sistemas corporativos de gestão de chamados (*ticketing*) e plataformas de acompanhamento de produtividade (*Task Management*), consolidando a carga de trabalho da engenharia.
*   **Visão Unificada (Single Pane of Glass):** Agregação de dados de infraestrutura e gestão num único painel, eliminando a necessidade de alternar entre múltiplas ferramentas durante o *troubleshooting* crítico.

---

## 3. Arquitetura e Stack Tecnológica

A aplicação adota uma arquitetura leve e escalável, focada em segurança, velocidade de resposta e facilidade de *deploy*.

*   **Backend (Maestro da API):** Desenvolvido em **Python 3** com o framework assíncrono **FastAPI**. Gere as conexões seguras aos motores de dados através de conectores nativos otimizados (PyMySQL, PyODBC, Psycopg2).
*   **Camada de Segurança:** Proteção de todos os *endpoints* através de **JWT** (JSON Web Tokens) com controle de acessos baseado em perfis (RBAC - Admin / Operador / Leitura). Nenhuma credencial é exposta no código-fonte, utilizando injeção estrita por variáveis de ambiente.
*   **Frontend (Direct-to-API):** Interface construída com padrões web puros (HTML5, CSS3, Vanilla JS), sem dependência de *frameworks* pesados de compilação, garantindo *load times* na casa dos milissegundos. Utiliza *Chart.js* para renderização estatística de alta fidelidade.
*   **Motor de Inteligência Artificial:** Infraestrutura Dockerizada executando o Ollama Server em instâncias dedicadas.

---

## 4. O Fluxo de Diagnóstico da Pipeline de Dados

A arquitetura do pipeline de inferência foi desenhada para operar de forma transparente em *background*:

1.  **Deteção Contínua:** Uma rotina assíncrona varre a fila de tarefas do orquestrador num intervalo de *polling* pré-definido.
2.  **Extração e Sanitização:** Os logs de erro brutos gerados pelas aplicações falhas são extraídos e estruturados.
3.  **Inferência Autónoma:** O texto é submetido ao LLM local, que elabora uma análise técnica estruturada com a identificação exata da quebra no código e a proposta de solução.
4.  **Persistência e Sinalização:** A análise gerada é guardada no banco de dados operacional e o alerta é sinalizado visualmente na *dashboard* da equipa de engenharia.
