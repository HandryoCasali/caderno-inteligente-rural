# Modelo de Domínio

**Código:** DOC-004
**Categoria:** Domínio
**Versão:** 1.1
**Status:** Aprovado
**Última atualização:** 01/07/2026
**Responsável:** Handryo Casali

---

# Objetivo

Este documento descreve o modelo conceitual do domínio do **Caderno Inteligente Rural**.

Seu objetivo é representar os principais conceitos do negócio, seus relacionamentos e responsabilidades, independentemente da tecnologia utilizada.

Este documento representa o domínio do negócio, e não um modelo de banco de dados.

---

# Visão Geral

O domínio do **Caderno Inteligente Rural** é centrado na gestão do rebanho.

Todas as funcionalidades do MVP derivam do gerenciamento dos animais pertencentes à propriedade e do histórico de acontecimentos relacionados a eles.

O **Animal** é o principal agregado do domínio, sendo responsável por manter sua consistência, seu estado atual e seu histórico de vida.

---

# Entidades

## Propriedade

Representa a fazenda administrada pelo produtor.

### Responsabilidades

* Identificar a propriedade.
* Agrupar logicamente o rebanho.
* Armazenar a produção diária de leite.
* Servir como limite organizacional da aplicação.

### Observações

No MVP cada usuário possui apenas uma propriedade.

---

## Animal (Entidade Principal)

Representa um animal pertencente ao rebanho.

É a entidade mais importante do domínio e o principal Aggregate Root do sistema.

### Responsabilidades

* Manter suas informações cadastrais.
* Representar a projeção atual do histórico do animal.
* Possuir histórico completo de eventos.
* Garantir todas as regras de negócio relacionadas ao animal.
* Garantir a consistência entre seu estado atual e seu histórico.

---

## Evento

Representa um fato ocorrido durante a vida de um animal.

Eventos são registros permanentes e imutáveis do domínio.

Depois de registrados, representam fatos históricos e não o estado atual do animal.

O estado atual é obtido pela interpretação do histórico de eventos em conjunto com as regras de negócio.

Todo evento possui características comuns:

* Data da ocorrência
* Tipo
* Observação
* Fotos (opcional)
* Responsável pelo registro
* Data de criação

### EventoAnimal

Representa acontecimentos relacionados ao ciclo de vida do animal.

Exemplos:

* Entrada
* Venda
* Morte

### EventoReprodutivo

Representa acontecimentos relacionados ao ciclo reprodutivo.

Exemplos:

* Cio
* Prenhez
* Parto

> **Observação:** Conceitualmente, o domínio diferencia Eventos do Animal e Eventos Reprodutivos por questões de negócio e linguagem ubíqua. Entretanto, a implementação poderá utilizar uma única entidade de persistência (`Evento`) com um campo identificando seu tipo, desde que essa decisão não comprometa a clareza do domínio.

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
* Arrobas são apenas uma representação derivada para exibição.

---

## Dinheiro

Representa valores monetários utilizados pelo domínio.

Evita o uso direto de tipos primitivos e centraliza futuras regras de arredondamento, comparação e formatação.

---

# Agregados

## Agregado Animal

### Aggregate Root

Animal

### Objetos pertencentes ao agregado

* Eventos
* Informações reprodutivas
* Estado atual

### Responsabilidades

O Animal é responsável por:

* Garantir todas as invariantes relacionadas ao seu ciclo de vida.
* Garantir a consistência entre seu estado atual e o histórico registrado.
* Impedir estados inválidos.
* Ser o único ponto de acesso para alterações relacionadas ao seu domínio.

Nenhum evento poderá existir sem um Animal.

Todo acesso ao histórico deverá ocorrer através do Animal.

---

## Agregado Propriedade

### Aggregate Root

Propriedade

### Objetos pertencentes ao agregado

* ProduçãoDiáriaLeite

### Responsabilidades

A Propriedade representa o limite organizacional da fazenda.

Os Animais pertencem a uma Propriedade, porém constituem um agregado independente.

---

# Relacionamentos

* Uma Propriedade possui vários Animais.
* Um Animal pertence a exatamente uma Propriedade.
* Um Animal possui vários Eventos.
* Uma Propriedade possui vários registros de Produção Diária de Leite.

---

# Responsabilidades dos Agregados

Cada agregado será responsável por manter suas próprias regras de negócio e consistência.

Cada agregado expõe sua própria camada de aplicação, responsável por coordenar seus casos de uso.

### Agregado Animal

Casos de uso típicos:

* Cadastrar Animal
* Atualizar Animal
* Registrar Entrada
* Registrar Venda
* Registrar Morte
* Registrar Cio
* Registrar Prenhez
* Registrar Parto

### Agregado Propriedade

Casos de uso típicos:

* Registrar Produção Diária de Leite
* Consultar Dashboard

Essa organização mantém o domínio desacoplado e alinhado à arquitetura do projeto.

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
* Preservar os princípios arquiteturais do projeto.
* Ser validado antes da implementação.

---

# Histórico de Alterações

| Versão | Data       | Alteração                                                                                                                                                                                         |
| ------ | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.0    | 28/06/2026 | Criação do Modelo de Domínio e definição dos agregados do MVP.                                                                                                                                    |
| 1.1    | 01/07/2026 | Revisão arquitetural: Animal consolidado como principal Aggregate Root, alinhamento com o modelo de estados, separação entre agregados Propriedade e Animal e refinamento do conceito de Eventos. |
