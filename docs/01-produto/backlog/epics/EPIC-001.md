# EPIC-001 — Gestão do Rebanho

**Código:** EPIC-001
**Status:** Não iniciada
**Prioridade:** Alta
**Versão:** MVP

---

# Objetivo

Permitir que o produtor rural gerencie o rebanho da propriedade por meio do cadastro, consulta e manutenção dos animais.

Esta Epic representa o núcleo do domínio do **Caderno Inteligente Rural**, sendo a base para as demais funcionalidades do sistema.

---

# Valor de Negócio

Ao concluir esta Epic, o produtor será capaz de:

* cadastrar seus animais;
* consultar o rebanho;
* manter os dados cadastrais atualizados;
* visualizar a situação atual de cada animal.

As funcionalidades desta Epic servirão como base para os módulos de eventos, reprodução, produção de leite e indicadores.

---

# Escopo

Esta Epic contempla funcionalidades relacionadas ao gerenciamento dos animais pertencentes à propriedade.

Não fazem parte desta Epic:

* eventos do ciclo de vida;
* reprodução;
* produção de leite;
* indicadores;
* autenticação.

Essas funcionalidades são tratadas em Epics específicas.

---

# Features

| Código   | Nome                     | Status       |
| -------- | ------------------------ | ------------ |
| FEAT-001 | Gerenciamento de Animais | Não iniciada |

---

# Dependências

Esta Epic não possui dependências funcionais.

Ela representa o ponto de partida do desenvolvimento do domínio.

---

# Epics Dependentes

As seguintes Epics dependem da conclusão desta:

* EPIC-002 — Eventos do Animal
* EPIC-003 — Reprodução
* EPIC-004 — Produção de Leite (parcialmente)
* EPIC-005 — Dashboard

---

# Domínio Relacionado

## Aggregate Root

* Animal

## Entidades

* Animal

## Objetos de Valor

* Peso

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

# Critério de Conclusão da Epic

A Epic será considerada concluída quando:

* todas as Features estiverem concluídas;
* todas as User Stories estiverem implementadas;
* os critérios de aceite das Features forem atendidos;
* a documentação relacionada estiver atualizada;
* os testes previstos forem aprovados.

---

# Histórico de Alterações

| Versão | Data       | Alteração                          |
| ------ | ---------- | ---------------------------------- |
| 1.0    | 01/07/2026 | Criação da Epic Gestão do Rebanho. |
