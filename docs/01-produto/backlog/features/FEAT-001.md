# FEAT-001 — Gerenciamento de Animais

**Código:** FEAT-001
**Epic:** EPIC-001 — Gestão do Rebanho
**Status:** Não iniciada
**Prioridade:** Alta
**Versão:** MVP

---

# Objetivo

Permitir que o produtor rural realize o gerenciamento completo dos animais pertencentes à sua propriedade.

Esta Feature representa o núcleo funcional do sistema e servirá como base para todas as funcionalidades relacionadas ao ciclo de vida do rebanho.

---

# Valor de Negócio

Ao concluir esta Feature, o produtor será capaz de:

* cadastrar animais;
* consultar o rebanho;
* visualizar os detalhes de cada animal;
* manter os dados cadastrais atualizados.

As informações registradas nesta Feature serão utilizadas pelos módulos de eventos, reprodução, produção de leite e dashboard.

---

# Escopo

Esta Feature contempla:

* cadastro de animais;
* consulta do rebanho;
* consulta detalhada de um animal;
* atualização dos dados cadastrais.

Não fazem parte desta Feature:

* registro de eventos;
* reprodução;
* produção de leite;
* indicadores.

---

# User Stories

| Código | Descrição                    | Status       |
| ------ | ---------------------------- | ------------ |
| US-001 | Cadastrar Animal             | Não iniciada |
| US-002 | Consultar Animais            | Não iniciada |
| US-003 | Consultar Detalhes do Animal | Não iniciada |
| US-004 | Atualizar Cadastro do Animal | Não iniciada |

---

# Regras de Negócio Relacionadas

Esta Feature deve respeitar todas as regras descritas na DOC-005 relacionadas ao cadastro e manutenção dos animais.

---

# Casos de Uso

Os seguintes casos de uso serão implementados:

* CadastrarAnimalUseCase
* ConsultarAnimaisUseCase
* ConsultarDetalhesAnimalUseCase
* AtualizarAnimalUseCase

---

# Modelo de Domínio

## Aggregate Root

* Animal

## Entidades

* Animal

## Objetos de Valor

* Peso

---

# Arquitetura Relacionada

A implementação deverá seguir a arquitetura definida na DOC-007 e nas ADRs do projeto.

Principais componentes previstos:

* AnimalController
* AnimalApplication
* Use Cases da Feature
* AnimalRepository
* Implementação JPA do repositório

---

# Endpoints previstos

| Método | Endpoint               | Descrição                    |
| ------ | ---------------------- | ---------------------------- |
| POST   | `/api/v1/animals`      | Cadastrar animal             |
| GET    | `/api/v1/animals`      | Consultar animais            |
| GET    | `/api/v1/animals/{id}` | Consultar detalhes do animal |
| PUT    | `/api/v1/animals/{id}` | Atualizar cadastro do animal |

Os contratos da API serão detalhados durante a implementação.

---

# Critérios Gerais de Aceite

A Feature deverá:

* respeitar todas as regras de negócio do domínio;
* manter a consistência do agregado `Animal`;
* utilizar os casos de uso previstos;
* expor os endpoints definidos;
* documentar a API com OpenAPI.

---

# Definition of Done

A Feature será considerada concluída quando:

* todas as User Stories estiverem concluídas;
* todos os critérios de aceite forem atendidos;
* os testes unitários do backend estiverem implementados e aprovados;
* a documentação da API estiver atualizada;
* a revisão de código estiver concluída;
* a documentação relacionada estiver revisada, quando necessário.

---

# Documentação Relacionada

## Produto

* DOC-003 — Escopo do MVP

## Domínio

* DOC-004 — Modelo de Domínio
* DOC-005 — Regras de Negócio
* DOC-006 — Casos de Uso e Estados

## Arquitetura

* DOC-007 — Arquitetura da Solução

## ADRs

* ADR-002 — Clean Architecture Pragmática
* ADR-003 — Organização por Features
* ADR-004 — Animal como Aggregate Root
* ADR-005 — Comunicação entre Features
* ADR-006 — Estratégia de Persistência

---

# Histórico de Alterações

| Versão | Data       | Alteração                                    |
| ------ | ---------- | -------------------------------------------- |
| 1.0    | 01/07/2026 | Criação da Feature Gerenciamento de Animais. |
