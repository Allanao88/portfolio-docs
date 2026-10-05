# Orquestração e Observabilidade de Dados com Apache Airflow

## 1. O Desafio Arquitetural (O Legado)

O projeto nasceu da necessidade crítica de garantir a replicação e a integridade dos dados para o **Data Warehouse** central da companhia. Inicialmente, a orquestração desta engenharia de dados (desenvolvida em Python) era gerida nativamente via `crontab` no Linux.

Apesar de funcional na sua conceção inicial, a abordagem *legacy* apresentava gargalos operacionais graves que limitavam a escala:
* **Falhas em Cascata:** O agrupamento era feito através de scripts `.sh` estritamente sequenciais. Se uma etapa de extração falhasse, toda a esteira subsequente era abortada, paralisando a atualização de dados.
* **Falta de Observabilidade (Caixa Preta):** A identificação da causa-raiz de uma falha exigia acesso manual via SSH à VM Linux para leitura de logs isolados em ficheiros de texto, aumentando drasticamente o MTTR (*Mean Time to Resolution*).

---

## 2. A Solução: Escala e Isolamento de Recursos

Para resolver os problemas de concorrência e visibilidade, a infraestrutura foi migrada para o **Apache Airflow**, operando num ambiente 100% conteinerizado (Docker) sobre uma máquina virtual **Rocky Linux**.

### ⚙️ Isolamento por Containers Efêmeros
Para mitigar a sobrecarga da máquina virtual, a arquitetura foi desenhada para lançar **containers efêmeros** no momento da execução de cada script. Este padrão de engenharia garante:
1. **Contenção de Falhas:** O *crash* ou o estouro de memória (OOM) de um script pesado de dados não afeta o *scheduler* central nem outros *pipelines* paralelos.
2. **Maximização de Recursos:** Prevenção de gargalos (*bottlenecks*) na VM *host*. Atualmente, o ecossistema orquestra **83 rotinas ativas** (desde ELT até rotinas semanais de DBA), suportando picos de **13 execuções simultâneas** sem degradação de performance do servidor.

---

## 3. Decisões de Engenharia (Stack Técnica)

* **Executor (`LocalExecutor`):** Escolhido estrategicamente para manter o controlo estrito dos recursos verticais da VM e simplificar a topologia da rede. Isto garante uma consolidação limpa dos logs, que agora são centralizados e facilmente consumidos pela UI nativa do Airflow.
* **Metadata Backend:** Banco de dados **PostgreSQL**, garantindo a persistência transacional fiável do estado das DAGs, histórico de execuções e registo de falhas.
* **Gestão de Credenciais:** As chaves de acesso a bases de dados e APIs (*connections*) não ficam expostas no código nem na interface web. São geridas através de variáveis de ambiente (`.env`) injetadas de forma segura nos containers no momento do *run*.
* **Ciclo de Deploy:** A gestão de *releases* ocorre de forma segmentada. Os scripts operacionais são alocados em diretórios mapeados no Rocky Linux e integrados a DAGs paramétricas, que dinamicamente orquestram a assiduidade necessária (de *cronjobs* por minuto a rotinas de manutenção semanais).

---

## 4. Inovação: Observabilidade e Auto-Diagnóstico com IA (LLM)

O grande diferencial competitivo desta implementação é a orquestração do *troubleshooting* aliada à Inteligência Artificial. 

Quando um *pipeline* sofre uma quebra, o diagnóstico técnico é realizado sem intervenção humana inicial:
1. **Varredura (Polling):** Um *pipeline* dedicado chamado `sys_observability_llm` faz a monitorização contínua das falhas geradas pelo sistema.
2. **Extração de Tracebacks:** Os trechos exatos de log (erros de compilação ou falhas de *timeout* em DBs) são recolhidos e inseridos numa tabela de auditoria no PostgreSQL.
3. **Inferência Local (Qwen2.5-Coder):** O motor de IA lê o *traceback* em base de dados, realiza a análise de *Root Cause* (RCA) e emite um parecer com a sugestão de correção do código, disponibilizando o resultado final diretamente no **Portal de Monitorização DBA**.
