# Linguagem Ubíqua

**Código:** DOC-003
**Categoria:** Domínio
**Versão:** 1.0
**Status:** Aprovado
**Última atualização:** 28/06/2026
**Responsável:** Handryo Casali

---

# Objetivo

Este documento define a linguagem oficial utilizada em todo o projeto.

Seu objetivo é garantir que todas as pessoas envolvidas utilizem os mesmos termos ao discutir regras de negócio, documentação, interface e implementação.

A linguagem definida aqui deverá ser utilizada em:

* Código-fonte
* Casos de uso
* APIs
* Banco de dados
* Documentação
* Interface do usuário

---

# Princípios

## Português do Brasil

Todo o domínio será escrito em Português do Brasil.

O objetivo é aproximar o código da linguagem utilizada pelos produtores rurais e facilitar o entendimento das regras de negócio.

Tecnologias, bibliotecas e frameworks poderão utilizar inglês, porém o domínio permanecerá em português.

---

# Glossário

## Animal

Representa um animal pertencente ao rebanho da propriedade.

É a principal entidade do domínio.

---

## Rebanho

Conjunto de animais pertencentes à propriedade.

No MVP existirá apenas um rebanho por propriedade.

---

## Propriedade

Local onde o rebanho está localizado.

No MVP cada usuário administra apenas uma propriedade.

---

## Evento

Registro histórico de um acontecimento relacionado a um animal.

Todo evento gera um histórico permanente.

Dependendo do tipo, também altera o estado atual do animal.

---

## Evento do Animal

Evento relacionado ao ciclo de vida do animal.

Exemplos:

* Entrada
* Venda
* Morte

---

## Evento Reprodutivo

Evento relacionado à reprodução.

Exemplos:

* Cio
* Prenhez
* Parto

---

## Entrada

Registro da chegada de um animal ao rebanho.

A origem poderá ser:

* Compra
* Nascimento
* Doação
* Outra

---

## Venda

Evento que registra a saída definitiva do animal por venda.

---

## Morte

Evento que registra a morte do animal.

O histórico deverá permanecer disponível.

---

## Cio

Evento que indica o início do ciclo reprodutivo da fêmea.

---

## Prenhez

Evento que confirma que a fêmea está prenha.

Um animal não poderá possuir duas prenhezes simultâneas.

---

## Parto

Evento que registra o nascimento de um bezerro.

No MVP o parto não cria automaticamente um novo animal.

O cadastro do novo animal será realizado manualmente pelo produtor.

---

## Status do Animal

Representa a situação atual do animal.

Exemplos:

* Ativo
* Vendido
* Morto

O status é derivado dos eventos registrados.

---

## Estado Reprodutivo

Representa a situação reprodutiva da fêmea.

Exemplos:

* Vazia
* Em cio
* Prenha

Esse estado é atualizado automaticamente pelos eventos reprodutivos.

---

## Brinco

Identificação física utilizada pelo produtor.

Não representa o identificador interno do sistema.

---

## Produção de Leite

Quantidade total de leite produzida pela propriedade em um determinado dia.

No MVP não será registrada por animal.

---

# Termos proibidos

Para manter consistência, os seguintes termos não deverão ser utilizados no domínio:

* Herd
* Livestock
* Pregnancy
* Birth
* Death
* Entity
* Model
* Record
* Register (como substantivo)

Sempre utilizar os equivalentes definidos neste documento.

---

# Convenções

## Classes

Devem utilizar substantivos do domínio.

Exemplos:

* Animal
* EventoAnimal
* EventoReprodutivo
* Propriedade

---

## Casos de Uso

Devem representar ações do produtor.

Exemplos:

* CadastrarAnimal
* RegistrarVenda
* RegistrarParto
* ConsultarRebanho

---

## Endpoints

Devem refletir o domínio.

Exemplos:

* /animais
* /animais/{id}/registrar-venda
* /animais/{id}/registrar-morte
* /animais/{id}/registrar-prenhez

---

## Interface

A interface deverá utilizar exatamente os mesmos termos definidos neste documento.

Não devem existir diferenças entre a linguagem utilizada pelo produtor e a linguagem utilizada pelo sistema.

---

# Evolução da Linguagem

Novos termos poderão ser adicionados conforme o domínio evoluir.

Sempre que um novo conceito surgir, este documento deverá ser atualizado antes da implementação.

---

# Histórico de Alterações

| Versão | Data       | Alteração                               |
| ------ | ---------- | --------------------------------------- |
| 1.0    | 28/06/2026 | Criação da Linguagem Ubíqua do projeto. |
