# DOC-006 — Estados e Transições

## Informações do Documento

| Campo                  | Valor                                                                        |
| ---------------------- | ---------------------------------------------------------------------------- |
| **Código**             | DOC-006                                                                      |
| **Categoria**          | Domínio                                                                      |
| **Versão**             | 1.0                                                                          |
| **Status**             | Draft                                                                        |
| **Autor**              | Handryo Casali                                                               |
| **Responsável**        | Handryo Casali                                                               |
| **Revisão Técnica**    | ChatGPT (Product Manager, Domain Expert, Software Architect, Tech Lead e QA) |
| **Data de Criação**    | 28/06/2026                                                                   |
| **Última Atualização** | 28/06/2026                                                                   |

---

# Objetivo

Definir os estados possíveis das principais entidades do domínio e as transições permitidas entre esses estados.

Este documento complementa as Regras de Negócio (DOC-005), servindo como referência para a implementação das validações, regras de consistência e comportamento da aplicação.

---

# Escopo

Este documento descreve:

* Estados do Animal.
* Estados Reprodutivos.
* Eventos que provocam mudanças de estado.

Não faz parte do escopo detalhar regras de negócio específicas, persistência de dados ou implementação técnica.

---

# Princípios do Modelo de Estados

Os estados descritos neste documento representam **a interpretação atual do histórico de eventos do domínio**.

O histórico de eventos é a **fonte da verdade** do sistema. Sempre que possível, o estado atual deve ser derivado desse histórico, evitando duplicação de informações e reduzindo o risco de inconsistências.

Por motivos de desempenho, a implementação poderá manter estados persistidos ou projetados, desde que eles possam ser reconstruídos integralmente a partir do histórico de eventos.

---

# 1. Estado do Animal

Todo animal possui um estado de situação.

## Estados

| Estado  | Descrição                                                |
| ------- | -------------------------------------------------------- |
| Ativo   | Animal pertence ao rebanho e pode receber novos eventos. |
| Vendido | Animal foi vendido e não pode receber novos eventos.     |
| Morto   | Animal morreu e não pode receber novos eventos.          |

---

## Diagrama

```text
                Cadastro
                    │
                    ▼
                ┌─────────┐
                │ Ativo   │
                └────┬────┘
                     │
        ┌────────────┴────────────┐
        ▼                         ▼
   ┌──────────┐              ┌─────────┐
   │ Vendido  │              │ Morto   │
   └────┬─────┘              └─────────┘
        │
        ▼
   ┌─────────┐
   │ Ativo   │
   └─────────┘
```

### Observações

* Um animal vendido pode retornar ao estado **Ativo**.
* Um animal morto representa um estado terminal.
* Animais vendidos ou mortos não podem receber novos eventos.

---

# 2. Estado Reprodutivo

O sistema acompanha apenas se existe ou não uma prenhez ativa.

## Estados

| Estado      | Descrição                            |
| ----------- | ------------------------------------ |
| Sem Prenhez | Situação padrão.                     |
| Prenhe      | Existe uma prenhez ativa registrada. |

---

## Diagrama

```text
           ┌───────────────┐
           │ Sem Prenhez   │
           └──────┬────────┘
                  │
             Evento Prenhez
                  │
                  ▼
             ┌──────────┐
             │ Prenhe   │
             └─────┬────┘
                   │
            Evento Parto
                   │
                   ▼
          ┌───────────────┐
          │ Sem Prenhez   │
          └───────────────┘
```

### Observações

* Uma prenhez pode ser registrada sem um cio anterior.
* Um parto encerra automaticamente uma prenhez ativa.
* Um parto pode ser registrado mesmo sem haver uma prenhez ativa registrada.

---

# 3. Eventos que provocam transições

## Situação do Animal

| Evento             | Origem           | Destino |
| ------------------ | ---------------- | ------- |
| Cadastro           | —                | Ativo   |
| Venda              | Ativo            | Vendido |
| Retorno ao Rebanho | Vendido          | Ativo   |
| Morte              | Ativo ou Vendido | Morto   |

## Estado Reprodutivo

| Evento  | Origem      | Destino     |
| ------- | ----------- | ----------- |
| Prenhez | Sem Prenhez | Prenhe      |
| Parto   | Prenhe      | Sem Prenhez |
| Parto   | Sem Prenhez | Sem Prenhez |

---

# 4. Estados Terminais

Os seguintes estados são considerados finais:

* Morto

Após atingir esse estado, nenhum novo evento poderá ser registrado para o animal.

---

# 5. Considerações para Implementação

* O estado atual do animal deverá ser derivado do histórico de eventos sempre que possível.
* O estado reprodutivo deverá refletir a sequência cronológica dos eventos reprodutivos registrados.
* Caso a aplicação mantenha estados persistidos para otimização de desempenho, eles deverão ser tratados como projeções do histórico e nunca como a fonte oficial da verdade.
* Toda alteração de estado deverá ser explicada por um evento registrado no histórico.

---

# Dependências

* DOC-001 — Manifesto
* DOC-003 — Linguagem Ubíqua
* DOC-004 — Modelo de Domínio
* DOC-005 — Regras de Negócio

---

# Documentos Relacionados

## Relacionados

* DOC-005 — Regras de Negócio

## Próximos

* Casos de Uso
* Backlog do MVP

---

# Histórico de Versões

| Versão | Data       | Autor          | Alterações      |
| ------ | ---------- | -------------- | --------------- |
| 1.0    | 28/06/2026 | Handryo Casali | Primeira versão |
