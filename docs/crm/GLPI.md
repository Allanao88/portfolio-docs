# ITSM, Governança de TI e Consolidação de Dados (GLPI)

## 1. Visão Executiva e Governança de Serviços

A maturidade de uma operação de TI mede-se pela sua capacidade de rastrear, priorizar e resolver incidentes de forma sistémica. 

Este documento detalha a arquitetura de *IT Service Management* (ITSM) implementada no **GLPI**, focando não apenas na parametrização do *Service Desk*, mas sobretudo na engenharia de dados construída para consolidar métricas de múltiplas instâncias num único ecossistema analítico.

---

## 2. Estruturação Arquitetural do Service Desk

Para garantir que os incidentes e requisições não fossem apenas "tickets isolados", mas sim processos governados, a plataforma foi estruturada com base nas melhores práticas:
* **Catálogo de Serviços:** Mapeamento e categorização de ponta a ponta dos serviços de TI, infraestrutura e operações, parametrizando a entrada de dados.
* **Gestão de Níveis de Serviço (SLA/OLA):** Implementação de regras temporais de tempo de resposta e tempo de resolução, assegurando o cumprimento de prazos contratuais consoante a prioridade do negócio.
* **Roteamento Inteligente:** Criação de matrizes de decisão operacionais para atribuição e escalonamento automático de chamados com base na categoria, urgência e criticidade do impacto.

---

## 3. Engenharia de Dados: Pipeline Multi-Instância

O maior desafio de arquitetura desta operação não era gerir uma ferramenta, mas sim resolver a fragmentação da informação. A infraestrutura da empresa opera com **4 instâncias independentes de GLPI**.

Para eliminar estes silos de dados, foi desenhada uma arquitetura de integração de alto nível:
* **Pipeline de Unificação (ETL):** Desenvolvimento de uma esteira de dados customizada que extrai os registos, metadados e tempos de atendimento das 4 instâncias de forma contínua.
* **Repositório Centralizado (MySQL):** Todos os dados extraídos são normalizados e persistidos num único banco de dados relacional. Esta consolidação atua como a *Single Source of Truth* (Fonte Única da Verdade) para toda a gestão de suporte corporativo.

---

## 4. Observabilidade e Business Intelligence

Ao transferir os dados das bases distribuídas do GLPI para um modelo centralizado, desbloqueámos capacidades analíticas avançadas (Data-Driven ITSM):
* **Grafana:** Conexão direta à base MySQL central para renderização de *dashboards* operacionais em tempo real (painéis de NOC), permitindo acompanhar o *backlog*, a volumetria de incidentes e a disponibilidade de ativos.
* **Power BI e Integrações (Excel):** Consumo dos modelos relacionais para construção de relatórios executivos táticos. Permite o cruzamento de KPIs de produtividade (Tempo Médio de Atendimento, SLA cumprido vs. violado) e a identificação de tendências estruturais de falhas.
