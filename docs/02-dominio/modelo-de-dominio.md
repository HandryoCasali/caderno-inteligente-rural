# Modelo de Domínio

**Código:** DOC-004
**Categoria:** Domínio
**Versão:** 1.0
**Status:** Aprovado
**Última atualização:** 28/06/2026
**Responsável:** Handryo Casali

---

# Objetivo

Este documento descreve o modelo conceitual do domínio do **Caderno Inteligente Rural**.

Seu objetivo é representar os principais conceitos do negócio, seus relacionamentos e responsabilidades, independentemente da tecnologia utilizada.

Este documento representa o domínio do negócio, e não um modelo de banco de dados.

---

# Visão Geral

No MVP, o sistema possui um único **Bounded Context**:

## Gestão do Rebanho

Esse contexto é responsável pelo gerenciamento dos animais da propriedade, seus eventos, seu estado atual e, para o gado leiteiro, pelo acompanhamento do ciclo reprodutivo e da produção diária de leite.

Todo o restante do sistema deriva desse contexto.

---

# Entidades

## Propriedade

Representa a fazenda administrada pelo produtor.

### Responsabilidades

* Identificar a propriedade.
* Agrupar o rebanho.
* Armazenar a produção diária de leite.
* Servir como limite organizacional do domínio.

### Observações

No MVP cada usuário possui apenas uma propriedade.

---

## Animal (Entidade Principal)

Representa um animal pertencente ao rebanho.

É a entidade mais importante do domínio.

### Responsabilidades

* Manter suas informações cadastrais.
* Representar o estado atual do animal.
* Possuir histórico completo de eventos.
* Possuir histórico reprodutivo.
* Garantir suas regras de negócio.

---

## Evento

Representa um acontecimento ocorrido durante a vida de um animal.

Todo evento possui características comuns:

* Data
* Tipo
* Observação
* Fotos (opcional)
* Responsável pelo registro
* Data de criação

No domínio existem atualmente duas especializações desse conceito.

### EventoAnimal

Eventos relacionados ao ciclo de vida do animal.

Tipos:

* Entrada
* Venda
* Morte

Responsabilidades:

* Registrar histórico permanente.
* Atualizar o Status do Animal quando necessário.

### EventoReprodutivo

Eventos relacionados à reprodução.

Tipos:

* Cio
* Prenhez
* Parto

Responsabilidades:

* Registrar histórico permanente.
* Atualizar o Estado Reprodutivo.
* Permitir validações específicas do domínio.

> **Observação:** No MVP, `EventoAnimal` e `EventoReprodutivo` serão implementados como entidades distintas. Conceitualmente, ambos representam especializações do conceito de **Evento**, o que poderá orientar futuras evoluções do domínio.

---

## ProduçãoDiáriaLeite

Representa a quantidade total de leite produzida pela propriedade em uma determinada data.

### Responsabilidades

* Registrar produção diária.
* Permitir consultas históricas.
* Apoiar futuras funcionalidades financeiras.

---

# Objetos de Valor

## Peso

Representa o peso do animal.

Características:

* Unidade oficial: quilogramas (kg).
* Arrobas são uma representação derivada para exibição.

---

## Dinheiro

Representa valores monetários utilizados pelo domínio.

Evita o uso direto de tipos primitivos e centraliza futuras regras de arredondamento e formatação.

---

# Agregados

## Agregado Animal

### Aggregate Root

Animal

### Objetos pertencentes ao agregado

* EventoAnimal
* EventoReprodutivo

### Responsabilidades

O Animal é responsável por garantir todas as invariantes relacionadas aos seus eventos.

Nenhum evento poderá existir sem um Animal.

Todo acesso aos eventos deverá ocorrer através do Animal.

---

## Agregado Propriedade

### Aggregate Root

Propriedade

### Objetos pertencentes ao agregado

* Animal
* ProduçãoDiáriaLeite

A Propriedade representa o limite organizacional do rebanho.

---

# Relacionamentos

Uma Propriedade possui vários Animais.

Um Animal possui vários Eventos do Animal.

Um Animal possui vários Eventos Reprodutivos.

Uma Propriedade possui vários registros de Produção Diária de Leite.

---

# Responsabilidades dos Agregados

Cada agregado será responsável por manter suas próprias regras de negócio e consistência.

Da mesma forma, cada agregado possuirá seus próprios Casos de Uso.

Exemplos:

### Agregado Animal

* Cadastrar Animal
* Atualizar Animal
* Registrar Entrada
* Registrar Venda
* Registrar Morte
* Registrar Cio
* Registrar Prenhez
* Registrar Parto

### Agregado Propriedade

* Consultar Dashboard
* Registrar Produção Diária de Leite

Essa organização mantém o domínio desacoplado e alinhado à arquitetura definida para o projeto.

---

# Limites do Domínio (MVP)

Não fazem parte deste contexto, neste momento:

* Vacinação
* Inseminação
* Controle sanitário
* Controle de medicamentos
* Controle de estoque
* Financeiro avançado
* Gestão de múltiplas propriedades

Esses conceitos poderão ser adicionados em futuras versões do produto.

---

# Evolução do Domínio

O domínio deverá evoluir de forma incremental.

Toda nova entidade ou conceito deverá:

* Respeitar o Manifesto.
* Utilizar a Linguagem Ubíqua.
* Integrar-se ao Modelo de Domínio.
* Ser validado antes da implementação.

---

# Histórico de Alterações

| Versão | Data       | Alteração                                                      |
| ------ | ---------- | -------------------------------------------------------------- |
| 1.0    | 28/06/2026 | Criação do Modelo de Domínio e definição dos agregados do MVP. |
