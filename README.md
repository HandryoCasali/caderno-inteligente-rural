# 🐂 Caderno Inteligente Rural

> **Transformando anotações em decisões.**

O **Caderno Inteligente Rural** é um SaaS para pequenos e médios produtores rurais brasileiros, criado para simplificar a gestão do rebanho por meio de uma experiência intuitiva e orientada à tomada de decisão.

> **O produtor já faz as anotações. Nosso objetivo é transformá-las em informações que facilitem a tomada de decisão.**

---

# 📑 Índice

* [Sobre o Projeto](#-sobre-o-projeto)
* [Objetivo](#-objetivo)
* [Público-Alvo](#-público-alvo)
* [Funcionalidades](#-funcionalidades-previstas)
* [Arquitetura](#️-arquitetura)
* [Documentação](#-documentação)
* [Roadmap](#-roadmap)
* [Telas](#-telas)
* [Filosofia de Desenvolvimento](#-filosofia-de-desenvolvimento)
* [Contribuição](#-contribuição)
* [Licença](#-licença)

---

# 📖 Sobre o Projeto

O controle do rebanho ainda é realizado, em muitos casos, utilizando cadernos, planilhas ou apenas a memória do produtor.

Essa realidade dificulta responder perguntas importantes do dia a dia, como:

* Quantas cabeças existem atualmente?
* Quais animais foram vendidos?
* Quais vacas estão prenhas?
* Há quanto tempo determinado animal está na propriedade?
* Quantos animais nasceram na fazenda?

O **Caderno Inteligente Rural** nasceu para resolver esse problema.

A proposta não é construir um ERP complexo, mas um **caderno digital inteligente**, simples de usar e capaz de transformar registros em informações úteis para o produtor rural.

---

# 🎯 Objetivo

Construir um sistema intuitivo, acessível e focado em pequenos e médios produtores rurais, permitindo registrar informações do rebanho em poucos segundos e consultar indicadores importantes sempre que necessário.

---

# 👨‍🌾 Público-Alvo

O produto é destinado, inicialmente, a produtores rurais brasileiros que:

* possuem até aproximadamente 200 cabeças;
* trabalham com gado de corte e/ou leite;
* administram uma única propriedade;
* utilizam cadernos, planilhas ou memória para controlar o rebanho;
* buscam uma solução simples, prática e intuitiva.

---

# ✨ Funcionalidades Previstas

## Controle do Rebanho

* Cadastro de animais
* Consulta do rebanho
* Histórico de eventos
* Registro de entrada
* Registro de venda
* Registro de morte

## Reprodução (Gado Leiteiro)

* Registro de cio
* Registro de confirmação de prenhez
* Registro de parto
* Alertas baseados na reprodução

## Dashboard

* Total de animais
* Animais ativos
* Animais por sexo
* Animais por finalidade
* Resumo do rebanho

## Evoluções Futuras

* Produção diária de leite
* Controle financeiro
* Alertas inteligentes
* Funcionamento offline
* Múltiplas propriedades
* Assistente com Inteligência Artificial

---

# 🏗️ Arquitetura

O projeto será desenvolvido utilizando princípios de **Domain-Driven Design (DDD)** e **Arquitetura Limpa**, priorizando simplicidade, clareza e evolução incremental.

## Backend

* Java 21
* Spring Boot
* PostgreSQL
* Redis (quando necessário)

## Frontend

* Angular
* Mobile First
* Progressive Web App (PWA)

## Infraestrutura

* AWS

---

# 📚 Documentação

Toda a documentação do projeto está organizada na pasta `docs/`.

Ela contém:

* Manifesto
* Visão do Produto
* Personas
* Linguagem Ubíqua
* Modelo de Domínio
* Arquitetura
* Funcionalidades
* Backlog
* Wireframes
* Templates
* Prompts para IA

Toda funcionalidade será especificada antes de ser implementada.

---

# 🛣️ Roadmap

* ✅ Descoberta do problema
* ✅ Definição do MVP
* ✅ Modelagem inicial do domínio
* 🔄 Documentação funcional
* ⏳ Desenvolvimento do Backend
* ⏳ Desenvolvimento do Frontend
* ⏳ Testes com produtores
* ⏳ Lançamento do MVP

---

# 📱 Telas

> Em desenvolvimento.

Os primeiros wireframes e mockups serão disponibilizados nesta seção durante a evolução do projeto.

---

# 🚀 Filosofia de Desenvolvimento

O projeto segue alguns princípios fundamentais:

* Transformar anotações em decisões.
* O sistema deve ser mais simples que um caderno.
* Especificar antes de implementar.
* Validar continuamente com produtores reais.
* Priorizar simplicidade.
* Toda informação cadastrada deve gerar valor.
* O domínio orienta a tecnologia.
* A documentação faz parte do produto.

---

# 🤝 Contribuição

Atualmente este projeto está sendo desenvolvido por um único desenvolvedor, utilizando ferramentas de Inteligência Artificial como apoio na especificação, arquitetura, documentação e implementação.

---

# 📄 Licença

Este projeto utiliza a licença MIT.
