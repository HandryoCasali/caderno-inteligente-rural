# Arquitetura da Solução

**Código:** DOC-007
**Categoria:** Arquitetura
**Versão:** 1.0
**Status:** Em elaboração
**Última atualização:** 01/07/2026
**Responsável:** Handryo Casali

---

# Objetivo

Este documento descreve a arquitetura de software adotada pelo **Caderno Inteligente Rural**.

Seu objetivo é servir como referência para o desenvolvimento da aplicação, documentando sua organização, os princípios arquiteturais, a comunicação entre módulos e as tecnologias adotadas.

As decisões arquiteturais detalhadas encontram-se registradas nas respectivas ADRs deste projeto.

---

# Visão Geral

O **Caderno Inteligente Rural** será desenvolvido como um **Monólito Modular**, organizado por **Features** e estruturado utilizando uma abordagem de **Clean Architecture Pragmática**.

A aplicação será composta por um único backend, um único banco de dados e um único frontend, mantendo separação lógica entre os diferentes domínios do negócio.

Essa abordagem busca equilibrar:

* simplicidade de desenvolvimento;
* baixo custo operacional;
* facilidade de manutenção;
* escalabilidade evolutiva;
* organização orientada ao domínio.

---

# Princípios Arquiteturais

A arquitetura do projeto é guiada pelos seguintes princípios.

## Organização orientada ao domínio

A estrutura do código deve refletir os conceitos do negócio.

As Features representam funcionalidades do domínio e não camadas técnicas.

---

## Baixo acoplamento

Cada módulo deve possuir responsabilidades bem definidas e depender do menor número possível de outros módulos.

---

## Alta coesão

Classes pertencentes à mesma funcionalidade devem permanecer agrupadas.

Cada Feature deve concentrar tudo o que é necessário para sua implementação.

---

## Clean Architecture Pragmática

As regras de negócio permanecem isoladas da infraestrutura.

Ao mesmo tempo, evita-se a criação de abstrações que não tragam benefícios reais para o projeto.

---

## Evolução incremental

A arquitetura deve permitir a inclusão de novas funcionalidades sem exigir grandes refatorações.

O projeto prioriza soluções simples e evolutivas.

---

## Independência tecnológica

O domínio não deve depender de frameworks, banco de dados ou detalhes de infraestrutura.

Mudanças tecnológicas devem causar o menor impacto possível nas regras de negócio.

---

# Decisões Arquiteturais

As principais decisões arquiteturais encontram-se registradas por meio dos Architecture Decision Records (ADR).

| ADR     | Decisão                                         |
| ------- | ----------------------------------------------- |
| ADR-001 | Arquitetura baseada em Monólito Modular         |
| ADR-002 | Clean Architecture Pragmática                   |
| ADR-003 | Organização do Código por Features              |
| ADR-004 | Animal como Aggregate Root Principal            |
| ADR-005 | Comunicação entre Features                      |
| ADR-006 | Estratégia de Persistência do Estado do Domínio |

A presente documentação complementa essas decisões, descrevendo como elas são aplicadas na solução.

---

# Visão Geral da Arquitetura

A arquitetura da solução pode ser representada da seguinte forma:

```text
Aplicativo Mobile / Web
        │
        ▼
Angular + Capacitor
        │
        ▼
REST API
        │
        ▼
Spring Boot
        │
        ▼
PostgreSQL
        │
        └────────► Amazon S3
```

O frontend comunica-se exclusivamente por meio da API REST.

A API é responsável por orquestrar os casos de uso do domínio e persistir as informações no banco de dados.

Arquivos enviados pelos usuários serão armazenados no Amazon S3.

---

# Objetivos da Arquitetura

A arquitetura foi projetada para atender aos seguintes objetivos:

* facilitar manutenção;
* reduzir acoplamento;
* preservar o domínio;
* permitir evolução contínua;
* simplificar testes;
* favorecer reutilização de componentes;
* manter clareza na organização do código.

---

# Escopo

Este documento descreve:

* arquitetura da solução;
* organização do backend;
* organização das Features;
* fluxo de execução;
* comunicação entre módulos;
* estratégia de persistência;
* API REST;
* stack tecnológica;
* estratégia de testes.

Os detalhes específicos de implementação encontram-se nas ADRs e nos documentos complementares do projeto.

# Organização da Solução

O projeto está organizado em três grandes áreas:

```text
caderno-inteligente-rural/

├── backend/
├── frontend/
├── docs/
├── .github/
├── README.md
└── docker-compose.yml
```

## Backend

Contém toda a API REST, regras de negócio, persistência e integrações.

## Frontend

Contém a aplicação Angular utilizada pelos usuários finais, preparada para execução Web e Mobile através do Capacitor.

## Docs

Centraliza toda a documentação funcional, arquitetural e de produto do projeto.

---

# Organização do Backend

O backend segue os princípios definidos nas ADRs:

* ADR-001 — Monólito Modular
* ADR-002 — Clean Architecture Pragmática
* ADR-003 — Organização por Features

Sua estrutura principal é:

```text
src/main/java/br/com/cadernointeligenterural/

├── animal/
├── propriedade/
├── usuario/
├── autenticacao/
├── dashboard/
└── shared/
```

Cada diretório representa uma **Feature** do domínio.

A criação de uma nova Feature deve representar um novo contexto funcional do sistema e não apenas uma nova entidade do banco de dados.

---

# Organização das Features

Cada Feature possui autonomia organizacional e concentra todos os componentes necessários para sua implementação.

Estrutura padrão:

```text
animal/

├── api/
├── application/
├── domain/
├── infrastructure/
└── config/
```

Essa organização favorece alta coesão, baixo acoplamento e facilita a evolução do sistema.

---

# Responsabilidade das Camadas

## API

Responsável pela comunicação com clientes externos.

Contém:

* Controllers
* DTOs
* Mappers de entrada e saída
* Validações de requisição

A camada de API não implementa regras de negócio.

---

## Application

Representa a interface pública da Feature.

Contém:

* Application Services
* Use Cases

É responsável por:

* orquestrar os casos de uso;
* controlar transações;
* recuperar agregados;
* persistir alterações;
* coordenar chamadas entre Features.

A camada Application não contém regras de negócio do domínio.

---

## Domain

Representa o núcleo da Feature.

Contém:

* Entidades
* Aggregate Roots
* Value Objects
* Domain Services
* Interfaces de Repository
* Regras de negócio

Toda regra de negócio deve ser implementada nesta camada.

O domínio não possui dependência de frameworks ou tecnologias específicas.

---

## Infrastructure

Implementa os detalhes técnicos necessários para suportar o domínio.

Contém:

* Repositories JPA
* Persistência
* Integrações externas
* Configurações específicas da infraestrutura

A infraestrutura depende do domínio, mas o domínio não depende da infraestrutura.

---

## Config

Contém configurações específicas da Feature.

Seu uso deve ser excepcional.

Configurações compartilhadas entre múltiplas Features devem permanecer na configuração global da aplicação.

---

# Exemplo de Organização de uma Feature

Abaixo está um exemplo simplificado da estrutura esperada para a Feature **Animal**.

```text
animal/

├── api/
│   ├── AnimalController
│   ├── request/
│   ├── response/
│   └── mapper/
│
├── application/
│   ├── AnimalApplication
│   └── usecase/
│       ├── CadastrarAnimalUseCase
│       ├── RegistrarVendaUseCase
│       ├── RegistrarPrenhezUseCase
│       └── RegistrarPartoUseCase
│
├── domain/
│   ├── model/
│   │   ├── Animal
│   │   ├── EventoAnimal
│   │   ├── EventoReprodutivo
│   │   └── Peso
│   │
│   ├── repository/
│   └── service/
│
├── infrastructure/
│   ├── persistence/
│   └── mapper/
│
└── config/
```

Essa estrutura deverá servir como referência para todas as Features do projeto.

---

# Shared

A pasta `shared` destina-se exclusivamente a componentes verdadeiramente compartilhados entre múltiplas Features.

Exemplos:

* tratamento global de exceções;
* filtros HTTP;
* configurações globais;
* utilitários genéricos;
* componentes transversais (*cross-cutting concerns*).

Antes de adicionar qualquer componente ao `shared`, deve-se avaliar se ele realmente pertence a mais de uma Feature.

O objetivo é evitar a criação de um módulo genérico excessivamente grande e fortemente acoplado.

# Fluxo de Execução

Toda funcionalidade do sistema deve seguir um fluxo previsível e consistente.

O objetivo é garantir:

* separação de responsabilidades;
* baixo acoplamento;
* facilidade de manutenção;
* clareza na execução dos casos de uso.

---

# Fluxo Geral de uma Requisição

Uma requisição percorre a aplicação da seguinte forma:

```text id="c1vkj5"
Cliente

↓

Controller

↓

Application Service

↓

Use Case

↓

Domínio

↓

Repository

↓

PostgreSQL

↓

Resposta
```

Cada camada possui uma responsabilidade específica.

---

# Controller

A camada de API recebe a requisição HTTP.

Responsabilidades:

* receber requisições;
* validar parâmetros;
* converter DTOs;
* invocar a camada Application;
* retornar respostas HTTP.

O Controller não implementa regras de negócio.

---

# Application Service

Representa a interface pública da Feature.

Responsabilidades:

* iniciar transações;
* coordenar casos de uso;
* integrar diferentes componentes;
* controlar o fluxo da operação.

O Application Service funciona como uma fachada para os casos de uso da Feature.

---

# Use Case

Representa uma ação específica do sistema.

Exemplos:

* Cadastrar Animal
* Registrar Venda
* Registrar Morte
* Registrar Prenhez
* Registrar Parto

Cada Use Case deve possuir uma única responsabilidade.

Responsabilidades:

* recuperar agregados;
* executar regras de negócio;
* persistir alterações;
* produzir o resultado da operação.

---

# Domínio

Representa o núcleo da aplicação.

Exemplo:

```text id="0ykj9h"
animal.registrarVenda(dataVenda)
```

O domínio é responsável por:

* validar regras;
* atualizar estados;
* garantir invariantes;
* manter consistência do agregado.

Toda regra de negócio deve residir nesta camada.

---

# Repository

Os Repositories representam a fronteira entre o domínio e a persistência.

Responsabilidades:

* recuperar agregados;
* persistir alterações;
* abstrair detalhes do banco de dados.

Os Repositories não implementam regras de negócio.

---

# Exemplo de Fluxo

Registro de venda de um animal.

```text id="7pv3y2"
HTTP POST

↓

AnimalController

↓

AnimalApplication

↓

RegistrarVendaUseCase

↓

AnimalRepository.buscar(id)

↓

Animal.registrarVenda()

↓

AnimalRepository.salvar()

↓

HTTP 200
```

Esse fluxo representa o padrão esperado para todas as operações do sistema.

---

# Comunicação entre Features

Conforme definido na ADR-005, uma Feature não pode acessar diretamente componentes internos de outra Feature.

Toda comunicação deve ocorrer pela camada Application.

---

## Fluxo Permitido

```text id="b8yxsn"
Feature Animal

↓

AnimalApplication

↓

PropriedadeApplication

↓

Feature Propriedade
```

---

## Fluxo Proibido

```text id="lq66gr"
AnimalRepository

↓

PropriedadeRepository
```

---

```text id="2w96ti"
Animal Domain

↓

Propriedade Infrastructure
```

---

```text id="7l6ph3"
Animal Use Case

↓

Propriedade Entity
```

Essas dependências violam o encapsulamento dos módulos.

---

# Transações

As transações devem ser controladas pela camada Application.

Regra geral:

```text id="z1jmgw"
Application

↓

Use Case

↓

Domínio

↓

Persistência
```

O domínio não deve conhecer detalhes de transação.

---

# Tratamento de Exceções

As exceções de negócio devem ser geradas pelo domínio.

Exemplos:

* Animal já vendido.
* Animal já morto.
* Data inválida.
* Operação não permitida.

As exceções serão tratadas pela camada de API e convertidas para respostas HTTP apropriadas.

---

# Dependências Permitidas

O fluxo de dependência deve seguir a seguinte direção:

```text id="x0vxik"
API

↓

Application

↓

Domain

↓

Infrastructure
```

Nunca o inverso.

---

# Objetivo do Fluxo

A padronização do fluxo garante:

* previsibilidade;
* facilidade de manutenção;
* facilidade de testes;
* isolamento do domínio;
* baixo acoplamento.

Toda nova funcionalidade implementada no sistema deverá respeitar este fluxo arquitetural.
