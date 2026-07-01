# Architecture Decision Records (ADR)

## Objetivo

Esta pasta contém os **Architecture Decision Records (ADR)** do projeto **Caderno Inteligente Rural**.

Os ADRs registram decisões arquiteturais relevantes tomadas ao longo da evolução do produto.

Cada ADR documenta:

* O contexto da decisão.
* O problema que precisava ser resolvido.
* As alternativas consideradas.
* A decisão tomada.
* As consequências da decisão.

O objetivo é preservar o histórico arquitetural do projeto e facilitar o entendimento das escolhas realizadas ao longo do tempo.

---

# O que deve ser registrado como ADR

Uma ADR deve ser criada sempre que uma decisão impactar significativamente:

* Arquitetura da aplicação.
* Estrutura do domínio.
* Organização do código.
* Estratégia de persistência.
* Estratégia de integração.
* Segurança.
* Infraestrutura.
* Tecnologias adotadas.
* Forma de comunicação entre módulos.

Exemplos:

* Adoção de Monólito Modular.
* Adoção de Clean Architecture.
* Definição de Feature First.
* Alteração da estratégia de autenticação.
* Migração de banco de dados.
* Mudança do modelo arquitetural.

---

# O que NÃO deve ser registrado como ADR

Não devem gerar ADR:

* Correções de bugs.
* Ajustes de layout.
* Refatorações locais.
* Melhorias de desempenho sem impacto arquitetural.
* Alterações operacionais de baixa relevância.
* Decisões temporárias de desenvolvimento.

---

# Estrutura dos ADRs

Todos os ADRs devem seguir a seguinte estrutura:

```md
# ADR-XXX - Título

## Status

## Data

## Contexto

## Problema

## Decisão

## Alternativas Consideradas

## Consequências Positivas

## Consequências Negativas

## Impacto

## ADRs Relacionadas

## Referências
```

---

# Status Permitidos

Os ADRs devem utilizar um dos seguintes status:

| Status      | Descrição                   |
| ----------- | --------------------------- |
| Proposta    | Ainda em discussão          |
| Aceita      | Aprovada e adotada          |
| Substituída | Substituída por outra ADR   |
| Rejeitada   | Avaliada, porém não adotada |

---

# Convenção de Nomenclatura

Formato:

```text
ADR-001-monolito-modular.md
ADR-002-clean-architecture.md
ADR-003-feature-first.md
```

Regras:

* Utilizar numeração sequencial.
* Não reutilizar números.
* Utilizar nomes curtos e objetivos.
* Utilizar letras minúsculas e hífen.

---

# Alteração de Decisões

Os ADRs são documentos históricos.

Uma ADR aceita não deve ser alterada para refletir uma nova decisão arquitetural.

Caso uma decisão precise ser modificada:

1. Criar uma nova ADR.
2. Registrar a nova decisão.
3. Marcar a ADR anterior como **Substituída**.
4. Referenciar a nova ADR.

Exemplo:

```text
ADR-001 → Substituída por ADR-015
```

Dessa forma o histórico arquitetural permanece preservado.

---

# Fluxo de Criação

Sempre que uma decisão arquitetural relevante for identificada:

1. Avaliar se a decisão possui impacto estrutural.
2. Discutir alternativas.
3. Registrar a decisão em uma nova ADR.
4. Aprovar a ADR.
5. Atualizar a documentação relacionada.
6. Somente então iniciar a implementação.

---

# ADRs Existentes

| Código  | Título                                                   | Status |
| ------- | -------------------------------------------------------- | ------ |
| ADR-001 | Arquitetura baseada em Monólito Modular                  | Aceita |
| ADR-002 | Adoção da Clean Architecture                             | Aceita |
| ADR-003 | Organização utilizando Feature First                     | Aceita |
| ADR-004 | Animal como Aggregate Root principal                     | Aceita |
| ADR-005 | Comunicação entre Features pela camada Application       | Aceita |
| ADR-006 | Histórico de Eventos como registro permanente do domínio | Aceita |
| ADR-007 | Stack Tecnológica Oficial do Projeto                     | Aceita |

---

# Referências

* Architecture Decision Records — Michael Nygard
* Documenting Architecture Decisions
* Clean Architecture
* Domain-Driven Design
* Manifesto do Projeto (DOC-001)
