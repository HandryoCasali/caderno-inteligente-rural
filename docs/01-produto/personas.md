# Personas

**Código:** DOC-002
**Categoria:** Produto
**Versão:** 1.0
**Status:** Aprovado
**Última atualização:** 28/06/2026
**Responsável:** Handryo Casali

---

# Objetivo

Este documento descreve os principais perfis de usuários considerados durante o desenvolvimento do **Caderno Inteligente Rural**.

As personas representam comportamentos observados em produtores rurais e orientam decisões de produto, experiência do usuário, priorização do backlog e evolução das funcionalidades.

---

# Persona 1 — João (Produtor de Gado de Corte)

## Perfil

João representa o pequeno produtor de gado de corte.

Possui entre 50 e 200 cabeças, administra uma única propriedade e realiza grande parte do controle do rebanho utilizando um caderno ou apenas a memória.

Seu principal objetivo é manter o controle dos animais de forma simples, sem depender de sistemas complexos.

### Objetivos

* Saber quantos animais possui.
* Registrar entradas, vendas e mortes.
* Encontrar rapidamente um animal.
* Consultar o histórico do rebanho.
* Confiar nas informações registradas.

### Dores

* Perde tempo procurando anotações.
* Nem sempre sabe a quantidade exata de animais.
* Possui registros espalhados em diferentes cadernos.
* Esquece informações antigas.
* Tem dificuldade para consultar o histórico de um animal.

### Comportamento

* Utiliza o celular diariamente.
* Tem baixa familiaridade com sistemas complexos.
* Espera registrar um evento em poucos segundos.
* Valoriza simplicidade acima de quantidade de funcionalidades.

### Funcionalidades Prioritárias

1. Cadastro de animais.
2. Consulta do rebanho.
3. Registro de entrada.
4. Registro de venda.
5. Registro de morte.
6. Dashboard resumido.

### Cenário de Uso

João compra um novo animal. Em menos de um minuto ele deseja cadastrá-lo utilizando apenas as informações essenciais. Meses depois, ao vender esse animal, deseja registrar a venda rapidamente e manter o histórico disponível para futuras consultas.

---

# Persona 2 — Maria (Produtora de Gado Leiteiro)

## Perfil

Maria representa a pequena produtora de leite.

Além do controle do rebanho, ela acompanha constantemente o ciclo reprodutivo das vacas e utiliza essas informações para planejar a produção leiteira.

### Objetivos

* Controlar cio, prenhez e parto.
* Receber lembretes importantes relacionados à reprodução.
* Registrar a produção diária de leite.
* Acompanhar a expectativa financeira da produção.

### Dores

* Esquece datas importantes relacionadas à reprodução.
* Possui informações distribuídas em diferentes anotações.
* Tem dificuldade para acompanhar quais vacas estão prenhas.
* Não consegue estimar facilmente a produção futura.

### Comportamento

* Registra informações praticamente todos os dias.
* Consulta frequentemente o sistema.
* Valoriza alertas automáticos.
* Está disposta a registrar mais informações quando percebe benefício imediato.

### Funcionalidades Prioritárias

1. Registro de cio.
2. Registro de prenhez.
3. Registro de parto.
4. Alertas reprodutivos.
5. Produção diária de leite.
6. Dashboard da produção.

### Cenário de Uso

Maria registra que uma vaca ficou prenha. O sistema acompanha essa informação e, no momento adequado, alerta que a vaca deverá entrar no período de descanso da ordenha antes do parto.

---

# Comparativo das Personas

| Critério                             | João                     | Maria                |
| ------------------------------------ | ------------------------ | -------------------- |
| Principal atividade                  | Gado de Corte            | Gado Leiteiro        |
| Frequência de uso                    | Algumas vezes por semana | Diariamente          |
| Principal dispositivo                | Celular                  | Celular              |
| Tempo ideal para registrar um evento | Até 30 segundos          | Até 30 segundos      |
| Familiaridade com tecnologia         | Baixa                    | Baixa                |
| Principal necessidade                | Controle do rebanho      | Controle reprodutivo |
| Valor percebido                      | Organização              | Planejamento         |

---

# O que ambas as personas possuem em comum

Independentemente da atividade, ambos esperam que o sistema seja:

* Simples.
* Rápido.
* Confiável.
* Fácil de aprender.
* Fácil de consultar.
* Utilizável diretamente pelo celular.

---

# Impacto no Produto

As personas influenciam diretamente diversas decisões.

Como consequência:

* O cadastro deve conter apenas informações essenciais.
* O dashboard deve apresentar um resumo da propriedade.
* O histórico do animal deve ser facilmente acessível.
* A navegação deve exigir poucos toques.
* Funcionalidades complexas devem ser adicionadas apenas quando gerarem valor comprovado.

---

# Impacto no Design

A experiência do usuário deverá priorizar:

* Botões grandes para uso em campo.
* Alto contraste para utilização sob luz solar.
* Poucos elementos por tela.
* Fluxos curtos para cadastro.
* Informações mais importantes sempre visíveis.

---

# Revisão das Personas

Este documento deverá ser revisado sempre que novos aprendizados forem obtidos com produtores reais.

As personas devem evoluir junto com o produto.

---

# Histórico de Alterações

| Versão | Data       | Alteração                                             |
| ------ | ---------- | ----------------------------------------------------- |
| 1.0    | 28/06/2026 | Criação do documento e definição das personas do MVP. |
