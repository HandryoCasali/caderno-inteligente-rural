# Backlog do Produto

## Objetivo

Este diretório contém o backlog oficial do Caderno Inteligente Rural.

O backlog descreve todas as funcionalidades planejadas para o produto, organizadas de forma hierárquica e rastreável.

Seu objetivo é conectar produto, domínio, arquitetura e implementação.

---

# Estrutura do Backlog

O backlog é organizado em quatro níveis:

```text
Epic
    ↓
Feature
        ↓
User Story
            ↓
Task
```

## Epic

Representa um grande objetivo de negócio.

Exemplos:

* Gestão do Rebanho
* Reprodução
* Produção de Leite

---

## Feature

Representa uma funcionalidade de negócio pertencente a uma Epic.

Exemplos:

* Gerenciamento de Animais
* Eventos do Animal
* Produção de Leite

---

## User Story

Representa uma necessidade do usuário.

Formato:

> Como <tipo de usuário>,
> quero <objetivo>,
> para <benefício>.

---

## Task

Representa uma atividade técnica necessária para implementar uma User Story.

As Tasks não fazem parte desta documentação.

Devem ser gerenciadas na ferramenta de acompanhamento do projeto.

---

# Convenções

## Identificadores

| Tipo       | Prefixo | Exemplo  |
| ---------- | ------- | -------- |
| Epic       | EPIC-   | EPIC-001 |
| Feature    | FEAT-   | FEAT-001 |
| User Story | US-     | US-001   |
| Task       | TASK-   | TASK-001 |

---

# Prioridades

| Prioridade | Significado                       |
| ---------- | --------------------------------- |
| Alta       | Essencial para o MVP              |
| Média      | Importante para evolução          |
| Baixa      | Pode ser implementada futuramente |

---

# Status

| Status                      | Descrição                  |
| --------------------------- | -------------------------- |
| Não iniciada                | Ainda não começou          |
| Refinamento                 | Em análise                 |
| Pronta para desenvolvimento | Pode entrar na sprint      |
| Em desenvolvimento          | Implementação em andamento |
| Em revisão                  | Revisão de código          |
| Em testes                   | Validação funcional        |
| Concluída                   | Entregue                   |

---

# Rastreabilidade

Toda User Story deve possuir referência para:

* documentos de domínio;
* regras de negócio;
* ADRs relevantes;
* casos de uso;
* implementação correspondente.

---

# Estrutura dos Arquivos

```text
backlog/

├── README.md
├── epics/
└── features/
```

Cada Epic e Feature possui documentação própria.
