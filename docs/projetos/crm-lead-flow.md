# CRM Lead Flow | Gestão Comercial

[Consultar o CRM publicado](https://crm-lead-flow-five.vercel.app/){ .md-button .md-button--primary }

## Visão geral

O CRM Lead Flow é uma aplicação de gestão comercial desenvolvida para a AKS - Tech. A proposta é centralizar o acompanhamento de leads, contatos, empresas e oportunidades, conectando o processo comercial à gestão de produtos e estoque.

O sistema também serve como base modular para a evolução de uma solução que possa ser adaptada a diferentes clientes.

## Problema e objetivos

A operação comercial precisa manter informações de clientes e oportunidades organizadas, acompanhar etapas de vendas e relacionar produtos às negociações.

O projeto busca atender essas necessidades por meio de módulos independentes, regras de negócio centralizadas e persistência em banco de dados.

## Módulos funcionais

- **Visão geral:** indicadores e atalhos para as principais áreas do CRM.
- **Leads:** cadastro e acompanhamento de oportunidades ao longo do funil comercial.
- **Contatos:** organização das pessoas relacionadas ao processo comercial.
- **Empresas:** cadastro de informações das organizações.
- **Estoque:** cadastro de produtos e acompanhamento das movimentações.
- **Produtos por lead:** associação dos produtos às oportunidades comerciais.

## Arquitetura e tecnologias

| Camada | Tecnologia | Responsabilidade |
|---|---|---|
| Interface | React | Construção da aplicação por componentes |
| Linguagem | TypeScript | Tipagem e manutenção do código |
| Ferramentas de front-end | Vite | Desenvolvimento e build |
| Backend e persistência | Supabase / PostgreSQL | Dados, autenticação e operações de banco |
| Segurança de dados | Supabase Auth e RLS | Controle de sessão e autorização no banco |
| Hospedagem web | Vercel | Publicação da interface |

## Decisões de engenharia

### Arquitetura modular

As funcionalidades são separadas por domínio, mantendo páginas, tipos e lógica de acesso aos dados organizados por módulo. Essa abordagem reduz o acoplamento e facilita a depuração e a evolução do sistema.

### Autenticação e autorização

O projeto utiliza autenticação do Supabase e controle de acesso aos dados por políticas de Row Level Security (RLS). O modelo de acesso deve ser validado também no banco de dados, e não depender exclusivamente das restrições da interface.

### Integração entre vendas e estoque

Os produtos podem ser associados às oportunidades comerciais. A mudança de uma oportunidade para o estágio de venda ganha integra-se à lógica de movimentação do estoque, com operações transacionais implementadas no banco.

O saldo é calculado a partir do histórico de movimentações, e o custo médio é utilizado como critério de valorização dos produtos.

### Manutenibilidade

A separação das funcionalidades em módulos facilita a identificação de falhas e permite evoluir o CRM sem transformar o componente principal da aplicação em um monólito.

## Competências demonstradas

- Desenvolvimento de aplicações web com React e TypeScript.
- Modelagem relacional com PostgreSQL.
- Integração de front-end com serviços de backend.
- Autenticação, autorização e políticas RLS.
- Implementação de regras de negócio para vendas e estoque.
- Organização modular e manutenção de código.
- Publicação de aplicações web.

## Estado e próximos passos

O projeto possui módulos de leads, contatos, empresas, visão geral e estoque. A evolução contínua deve incluir testes de regressão, validação de fluxos críticos, refinamento da experiência de uso e revisão das regras de autorização antes da distribuição comercial.

## Demonstração

[CRM Lead Flow — aplicação publicada](https://crm-lead-flow-five.vercel.app/)

A demonstração pode exigir autenticação. Não disponibilize credenciais, dados reais de clientes ou informações internas no portfólio.

---

> Este case descreve a arquitetura e as funcionalidades implementadas no projeto. Indicadores de adoção, desempenho e retorno comercial devem ser incluídos somente após medição.
