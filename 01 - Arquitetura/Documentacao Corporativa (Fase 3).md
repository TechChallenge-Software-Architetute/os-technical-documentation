---
title: Documentação Corporativa — Fase 3
tags:
  - arquitetura
  - fase-3
  - rfc
  - adr
  - tech-challenge
aliases:
  - RFCs e ADRs
  - Fase 3
  - Documentação Arquitetural
---

# Documentação Corporativa — Fase 3

> [!info] Sobre esta nota
> A partir da Fase 3 (Tech Challenge), o sistema deixou de viver em um único
> repositório e passou a ser composto por **5 repositórios** com CI/CD
> independente. A documentação arquitetural formal (RFCs, ADRs, diagrama ER,
> diagramas de sequência) vive **nesses repositórios**, não neste vault —
> esta nota é o ponto de redirecionamento para cada um deles.

## Os 5 Repositórios

| Repositório | Responsabilidade | Link |
|---|---|---|
| `os-management` | Aplicação principal (Spring Boot) + manifests K8s | [GitHub](https://github.com/TechChallenge-Software-Architetute/os-management) |
| `os-management-gateway` | API Gateway (AWS API Gateway, Terraform) | [GitHub](https://github.com/TechChallenge-Software-Architetute/os-management-gateway) |
| `os-management-lambda` | Functions serverless de autenticação via CPF | [GitHub](https://github.com/TechChallenge-Software-Architetute/os-management-lambda) |
| `os-management-k8s-terraform` | VPC + EKS (Terraform) | [GitHub](https://github.com/TechChallenge-Software-Architetute/os-management-k8s-terraform) |
| `os-management-database` | RDS PostgreSQL (Terraform) + schema | [GitHub](https://github.com/TechChallenge-Software-Architetute/os-management-database) |

Justificativa de por que são 5 repositórios (e não os 4 citados no
enunciado) está registrada na ADR-0003 (link abaixo).

## RFCs — Request for Comments

Decisões técnicas avaliadas antes da implementação, vivem em
`os-management/docs/rfc/`
([PR docs/fase3-rfc-adr-arquitetura](https://github.com/TechChallenge-Software-Architetute/os-management/pull/new/docs/fase3-rfc-adr-arquitetura) —
pendente de merge para `develop`):

- [Índice de RFCs](https://github.com/TechChallenge-Software-Architetute/os-management/blob/docs/fase3-rfc-adr-arquitetura/docs/rfc/README.md)
- [RFC-0001 — Escolha do provedor de nuvem](https://github.com/TechChallenge-Software-Architetute/os-management/blob/docs/fase3-rfc-adr-arquitetura/docs/rfc/RFC-0001-escolha-provedor-nuvem.md)
- [RFC-0002 — Escolha do banco de dados gerenciado](https://github.com/TechChallenge-Software-Architetute/os-management/blob/docs/fase3-rfc-adr-arquitetura/docs/rfc/RFC-0002-escolha-banco-dados.md)
- [RFC-0003 — Estratégia de autenticação via CPF](https://github.com/TechChallenge-Software-Architetute/os-management/blob/docs/fase3-rfc-adr-arquitetura/docs/rfc/RFC-0003-estrategia-autenticacao.md)

## ADRs — Architecture Decision Records

Decisões arquiteturais permanentes, vivem em `os-management/docs/adr/`
(mesmo PR acima):

- [Índice de ADRs](https://github.com/TechChallenge-Software-Architetute/os-management/blob/docs/fase3-rfc-adr-arquitetura/docs/adr/README.md)
- [ADR-0001 — Padrão de comunicação entre componentes](https://github.com/TechChallenge-Software-Architetute/os-management/blob/docs/fase3-rfc-adr-arquitetura/docs/adr/ADR-0001-padrao-comunicacao.md)
- [ADR-0002 — Uso de HPA para escalabilidade horizontal](https://github.com/TechChallenge-Software-Architetute/os-management/blob/docs/fase3-rfc-adr-arquitetura/docs/adr/ADR-0002-uso-hpa.md)
- [ADR-0003 — Split em múltiplos repositórios](https://github.com/TechChallenge-Software-Architetute/os-management/blob/docs/fase3-rfc-adr-arquitetura/docs/adr/ADR-0003-split-multiplos-repositorios.md)
- [ADR-0004 — Arquitetura Hexagonal (Ports & Adapters)](https://github.com/TechChallenge-Software-Architetute/os-management/blob/docs/fase3-rfc-adr-arquitetura/docs/adr/ADR-0004-arquitetura-hexagonal.md)

> [!warning] Divergência com este vault
> A [[Padroes de Projeto]] e a [[Visao Geral]] deste vault descrevem o
> backend como **Vertical Slice Architecture (VSA)**. A ADR-0004 formaliza
> a organização **atual** do código (`os-management/src/main/java/...`)
> como **Arquitetura Hexagonal (Ports & Adapters)** — domínio, aplicação e
> adapters em camadas explícitas. Se o time confirmar que o código migrou
> de VSA para Hexagonal em algum momento da Fase 2/3, as notas de
> [[Visao Geral]] e [[Padroes de Projeto]] precisam ser atualizadas para
> não conflitar com a ADR.

## Diagramas de Arquitetura e de Sequência

Consolidados em `os-management/docs/architecture.md`:

- [Diagrama de Componentes — visão consolidada multi-repositório](https://github.com/TechChallenge-Software-Architetute/os-management/blob/docs/fase3-rfc-adr-arquitetura/docs/architecture.md#visão-consolidada-da-solução-multi-repositório) — API Gateway, Lambdas, EKS, RDS e Datadog em um único diagrama
- [Diagrama de Sequência — Autenticação via CPF](https://github.com/TechChallenge-Software-Architetute/os-management/blob/docs/fase3-rfc-adr-arquitetura/docs/architecture.md#autenticação-via-cpf)
- [Diagrama de Sequência — Abertura de Ordem de Serviço](https://github.com/TechChallenge-Software-Architetute/os-management/blob/docs/fase3-rfc-adr-arquitetura/docs/architecture.md#abertura-de-ordem-de-serviço)
- Diagrama de sequência da autenticação (fonte original, mais detalhado):
  [`os-management-lambda/README.md`](https://github.com/TechChallenge-Software-Architetute/os-management-lambda/blob/main/README.md#authentication-sequence)

## Modelagem do Banco de Dados

Vive em `os-management-database`
([PR docs/er-diagram-e-justificativa-banco](https://github.com/TechChallenge-Software-Architetute/os-management-database/pull/new/docs/er-diagram-e-justificativa-banco) —
pendente de merge para `main`):

- [Diagrama ER + explicação dos relacionamentos](https://github.com/TechChallenge-Software-Architetute/os-management-database/blob/docs/er-diagram-e-justificativa-banco/README.md#modelagem-do-banco-de-dados)
- [Justificativa formal da escolha do banco](https://github.com/TechChallenge-Software-Architetute/os-management-database/blob/docs/er-diagram-e-justificativa-banco/README.md#justificativa-da-escolha-do-banco-de-dados) (resumo — detalhe completo na RFC-0002 acima)
- [Ajustes propostos no modelo relacional](https://github.com/TechChallenge-Software-Architetute/os-management-database/blob/docs/er-diagram-e-justificativa-banco/README.md#ajustes-no-modelo-relacional-proposto) — FKs, índices e `CHECK` constraints ainda não aplicados ao schema em produção
- [Script `ddl-improvements.sql`](https://github.com/TechChallenge-Software-Architetute/os-management-database/blob/docs/er-diagram-e-justificativa-banco/scripts/ddl-improvements.sql)

## Infraestrutura Kubernetes

- [Diagrama de arquitetura do cluster (VPC + EKS + metrics-server)](https://github.com/TechChallenge-Software-Architetute/os-management-k8s-terraform/blob/docs/diagrama-arquitetura/README.md#architecture)
  ([PR docs/diagrama-arquitetura](https://github.com/TechChallenge-Software-Architetute/os-management-k8s-terraform/pull/new/docs/diagrama-arquitetura) — pendente de merge para `main`)

## Monitoramento e Observabilidade

- [`os-management/datadog/README.md`](https://github.com/TechChallenge-Software-Architetute/os-management/blob/develop/datadog/README.md) — APM, métricas de Kubernetes, healthchecks/uptime, logs correlacionados e métricas de negócio (volume de OS, tempo médio por status)

## Status de Entrega (Portal do Aluno)

Ainda pendentes neste momento (ver checklist completo no PDF do Tech
Challenge):

- [ ] Vídeo de demonstração da Fase 3 (o vídeo/roteiro atuais são da Fase 2)
- [ ] Documento PDF único para o Portal do Aluno com os links dos 5
      repositórios, vídeo e documentações
- [ ] Merge dos 3 Pull Requests linkados acima (`os-management`,
      `os-management-database`, `os-management-k8s-terraform`)
- [ ] Confirmação do usuário `soat-architecture` em todos os repositórios

## Links Relacionados
- [[Visao Geral]]
- [[Padroes de Projeto]]
- [[Ciclo de Vida da OS]]
