# GLPI 11 & Governança de Serviços de TI (ITSM)

Uma plataforma de Service Desk robusta é o que garante que a operação de uma empresa não pare. Minha vivência com o **GLPI** vai muito além do suporte diário ou parametrização básica: atuei no *core* da infraestrutura da ferramenta, liderando desafios de arquitetura e transição de sistemas.

O grande marco dessa trajetória foi atuar como **ponto focal técnico na configuração e migração corporativa para o GLPI 11**, um projeto que exigiu visão sistêmica, conhecimento em banco de dados e planejamento rigoroso para garantir *zero downtime* na operação.

---

## 🚀 O Desafio Técnico: Migração para o GLPI 11

Atualizar o sistema central de chamados e ativos de uma operação em andamento é um procedimento de alto risco. Como líder técnico dessa frente, fui responsável por orquestrar a transição de ponta a ponta:

* **Arquitetura e Infraestrutura:** Preparação do ambiente hospedeiro (`Linux`) e validação de requisitos sistêmicos, garantindo a compatibilidade de pacotes e extensões exigidas pela nova arquitetura da versão 11.
* **Integridade de Banco de Dados:** Tratativas prévias no banco de dados (`MySQL`) para assegurar que todo o histórico de chamados, base de conhecimento, SLAs e inventário de rede fossem migrados sem corrupção ou perda de dados.
* **Homologação e Rollout:** Mapeamento das regras de negócio legadas (perfis de usuário, fluxos de aprovação e matrizes de roteamento) para adequação aos novos padrões e automações nativas do GLPI 11.
* **Estabilização (Go-Live):** Atuação direta no troubleshooting pós-implantação, ajustando permissões e corrigindo desvios operacionais em tempo real para minimizar o impacto nos departamentos usuários.

## 🛠️ Integração, Automação e Observabilidade

Um sistema de chamados só atinge seu potencial máximo quando se torna transparente para a gestão. Para agregar inteligência ao GLPI, apliquei conceitos de dados e observabilidade:

* **Métricas em Tempo Real:** Conexão do banco de dados do GLPI com ferramentas de BI e monitoramento. Extraí e modelei dados para alimentar painéis no **Power BI** e dashboards operacionais no **Grafana**.
* **Gestão de SLAs e Gargalos:** A partir dos dashboards construídos, a gestão passou a ter visibilidade imediata sobre o volume de incidentes, tempo médio de resposta (TMA/TME) e eficiência das equipes de atendimento.
* **Automação de Workflows:** Parametrização avançada para garantir que incidentes de infraestrutura ou solicitações de rotina fossem direcionados automaticamente para as filas corretas, reduzindo o *overhead* do nível 1 (N1).

## 📊 Impacto de Negócio

* **Modernização Tecnológica:** Entrega de um ambiente ITSM atualizado, mais rápido, seguro e aderente às necessidades de escalabilidade da empresa.
* **Governança de Dados Baseada em Fatos:** A substituição do "achismo" operacional por indicadores visuais claros, permitindo dimensionamento correto de equipes e identificação rápida de problemas crônicos na infraestrutura.
* **Confiabilidade Operacional:** Garantia de que a esteira de suporte da empresa funcionasse de maneira fluida, estável e altamente rastreável.

---

> *"Liderar a migração de um sistema crítico exige mais do que seguir manuais; exige proteger os dados históricos, estabilizar a infraestrutura e garantir que, no dia seguinte, a operação acorde melhor do que foi dormir."*
