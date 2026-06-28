# DOC-005 — Regras de Negócio

**Código:** DOC-005
**Categoria:** Domínio
**Versão:** 1.0 (Draft)
**Status:** Em elaboração
**Última atualização:** 28/06/2026
**Autor:** Handryo Casali
**Revisão:** ChatGPT (Product Manager, Domain Expert, Software Architect, Tech Lead e QA)

---

# 1. Objetivo

Este documento define as regras de negócio do **Caderno Inteligente Rural**.

As regras aqui descritas representam o comportamento esperado do domínio e constituem a principal referência para implementação dos Casos de Uso, APIs, testes automatizados e futuras evoluções do sistema.

Sempre que existir divergência entre implementação e este documento, as regras aqui definidas deverão prevalecer.

---

# 2. Princípios do Domínio

Os princípios abaixo orientam todas as decisões de negócio do sistema.

## PD-001 — O sistema representa a realidade do produtor

O sistema deve adaptar-se à rotina do produtor rural, evitando impor fluxos rígidos que não reflitam o trabalho realizado na propriedade.

---

## PD-002 — O histórico é a fonte da verdade

Todo acontecimento relevante da vida de um animal deve ser registrado como um evento.

A situação atual do animal e seu estado reprodutivo são consequências do histórico de eventos registrados.

Caso um evento seja removido, o sistema deverá recalcular automaticamente todas as informações derivadas.

---

## PD-003 — Registro tardio é permitido

Os eventos poderão ser registrados após sua ocorrência real.

As regras do domínio considerarão sempre a **data do evento**, e não a data em que o registro foi realizado.

---

## PD-004 — O produtor possui a decisão final

Alertas e notificações têm caráter informativo.

O sistema nunca executará automaticamente ações de manejo sem uma confirmação explícita do produtor.

---

## PD-005 — Simplicidade acima da complexidade

O MVP prioriza funcionalidades essenciais para pequenos produtores.

Sempre que possível, o domínio deverá ser mantido simples, permitindo evolução gradual sem comprometer a consistência das regras existentes.

---

# 3. Convenções

Para garantir consistência entre todos os documentos do projeto, serão adotadas as seguintes convenções.

## Situação do Animal

Representa a condição do animal dentro da propriedade.

Valores possíveis:

* Ativo
* Vendido
* Morto

---

## Estado Reprodutivo

Representa a condição reprodutiva atual da fêmea.

Valores possíveis:

* Vazia
* Em Cio
* Prenha

---

## Evento

Todo fato relevante ocorrido na vida do animal deverá ser registrado como um evento.

Exemplos:

* Entrada
* Venda
* Morte
* Cio
* Prenhez
* Parto

---

# 4. Cadastro do Animal

## RN-001 — Todo animal pertence a uma única propriedade

### Descrição

Cada animal deverá estar vinculado a uma única propriedade rural.

Não é permitido que um mesmo animal pertença simultaneamente a mais de uma propriedade.

---

## RN-002 — Nome e brinco identificam o animal para o produtor

### Descrição

Os principais identificadores utilizados pelo produtor serão:

* Nome
* Brinco

Essas informações deverão facilitar a localização do animal durante as operações diárias.

---

## RN-003 — O cadastro inicial representa a entrada do animal

### Descrição

Ao cadastrar um novo animal, o sistema deverá registrar automaticamente um evento de Entrada correspondente.

Esse evento passa a integrar o histórico permanente do animal.

---

## RN-004 — Todo animal inicia com situação Ativa

### Descrição

Após o cadastro inicial, a situação do animal será considerada **Ativa**.

---

## RN-005 — A exclusão física de animais não é permitida

### Descrição

O sistema não realizará exclusão física de registros de animais.

Quando necessário, será utilizada exclusão lógica, preservando o histórico do domínio.

---

# 5. Ciclo de Vida do Animal

## RN-006 — A entrada ativa o animal

### Descrição

Ao registrar uma Entrada, a situação do animal passa para **Ativo**.

Caso o animal esteja vendido, a entrada representa seu retorno ao rebanho, preservando todo o histórico existente.

Não é permitido registrar entrada para um animal morto.

---

## RN-007 — A venda encerra temporariamente a permanência do animal na propriedade

### Descrição

Ao registrar uma Venda:

* a situação passa para **Vendido**;
* o evento permanece no histórico;
* o animal deixa de aceitar novos eventos, exceto uma nova Entrada.

---

## RN-008 — A morte encerra definitivamente o ciclo de vida do animal

### Descrição

Ao registrar uma Morte:

* a situação passa para **Morto**;
* o evento permanece no histórico;
* nenhum novo evento poderá ser registrado para o animal.

---

## RN-009 — O histórico determina a situação atual do animal

### Descrição

A situação atual do animal deverá ser sempre consistente com o histórico de eventos registrados.

Sempre que houver alteração no histórico, a situação deverá ser recalculada automaticamente.

---

## RN-010 — Correções de eventos são realizadas por exclusão e novo registro

### Descrição

No MVP, a correção de um evento ocorrerá por meio da exclusão do registro incorreto e do cadastramento de um novo evento.

Não haverá edição direta de eventos.

---

# 6. Reprodução

A reprodução é controlada por meio de eventos registrados no histórico do animal.

O sistema não exige que todos os acontecimentos sejam registrados em sequência, permitindo registros retroativos conforme a realidade da propriedade.

---

## RN-011 — O cio pode ser registrado múltiplas vezes

### Descrição

O sistema permitirá registrar mais de um evento de Cio consecutivamente para um mesmo animal.

### Motivação

Nem todo cio evolui para uma prenhez. O produtor deve conseguir registrar cada ocorrência observada sem restrições artificiais.

---

## RN-012 — A prenhez não depende de um cio registrado

### Descrição

O registro de Prenhez poderá ser realizado mesmo que não exista um evento anterior de Cio.

### Motivação

O produtor pode identificar a prenhez posteriormente, sem ter observado ou registrado o cio.

---

## RN-013 — O parto pode ser registrado independentemente de uma prenhez registrada

### Descrição

O sistema permitirá registrar um Parto mesmo que não exista uma prenhez ativa no histórico.

### Motivação

Nem toda prenhez é registrada pelo produtor, porém o parto representa um fato ocorrido e deve ser documentado.

---

## RN-014 — O parto encerra automaticamente uma prenhez ativa

### Descrição

Quando existir uma prenhez ativa para o animal, o registro de um Parto encerrará automaticamente esse estado reprodutivo.

Após o parto, o Estado Reprodutivo passa a ser **Vazia**.

---

## RN-015 — Eventos reprodutivos podem ser registrados retroativamente

### Descrição

Eventos de Cio, Prenhez e Parto poderão ser registrados após sua ocorrência, desde que a data informada represente corretamente o acontecimento.

### Motivação

Permitir que o histórico reflita a realidade da propriedade, mesmo quando os registros forem realizados dias ou meses depois.

---

## RN-016 — O evento de Parto representa apenas sua ocorrência

### Descrição

O evento de Parto registra apenas que houve um parto na data informada.

Não serão tratados no MVP cenários específicos como aborto, parto gemelar, natimorto ou complicações.

Essas informações poderão ser registradas no campo de observação do evento.

### Evolução futura

Caso essas situações passem a exigir regras específicas, poderão ser transformadas em novos tipos de eventos.

---

# 7. Produção de Leite

A produção de leite será controlada por propriedade, refletindo a realidade operacional dos pequenos produtores.

---

## RN-017 — A produção é registrada por propriedade

### Descrição

A produção diária de leite será registrada considerando a produção total da propriedade em uma determinada data.

Não haverá controle de produção individual por animal no MVP.

---

## RN-018 — Apenas um registro de produção por data

### Descrição

Cada propriedade poderá possuir apenas um registro de produção para cada data.

### Motivação

Evitar duplicidade de informações e simplificar o cálculo de indicadores e faturamento.

---

## RN-019 — A quantidade produzida deve ser maior que zero

### Descrição

A quantidade produzida deverá ser um valor positivo.

Caso não tenha ocorrido produção em determinada data, recomenda-se não registrar um lançamento.

---

## RN-020 — O valor recebido por litro é opcional

### Descrição

O produtor poderá informar posteriormente o valor recebido por litro de leite.

A ausência dessa informação não impede o registro da produção diária.

---

## RN-021 — O faturamento esperado é derivado

### Descrição

Quando houver quantidade produzida e valor por litro, o sistema poderá calcular automaticamente o faturamento esperado da produção.

Esse cálculo não substitui um controle financeiro futuro, servindo apenas como informação derivada.

---

## RN-022 — O histórico de produção é permanente

### Descrição

Todos os registros de produção passam a compor o histórico da propriedade.

Correções deverão ocorrer pela exclusão do registro incorreto e criação de um novo registro.

---

# 8. Consistência do Domínio

Esta seção define regras que garantem a integridade das informações independentemente da funcionalidade utilizada.

---

## RN-023 — A exclusão de animais é lógica

### Descrição

A exclusão de um animal deverá ocorrer por meio de exclusão lógica.

O histórico do animal permanecerá armazenado para preservar a rastreabilidade das informações.

### Critérios de Aceitação

* O animal não deverá aparecer nas listagens padrão.
* O histórico permanecerá íntegro.
* O animal poderá ser recuperado por consultas específicas, caso necessário.

---

## RN-024 — Apenas animais ativos podem ser excluídos

### Descrição

A exclusão lógica somente poderá ser realizada quando a Situação do Animal for **Ativo**.

Animais vendidos ou mortos fazem parte do histórico da propriedade e não poderão ser excluídos.

---

## RN-025 — A exclusão de eventos exige atualização das informações derivadas

### Descrição

Quando um evento for excluído, todas as informações derivadas do histórico deverão permanecer consistentes.

Exemplos:

* Situação do Animal.
* Estado Reprodutivo.
* Alertas relacionados.

---

## RN-026 — O alerta de sete meses de prenhez é apenas informativo

### Descrição

Quando uma prenhez atingir sete meses, o sistema deverá gerar um alerta ao produtor recomendando interromper a ordenha.

O alerta não altera automaticamente nenhuma informação do domínio.

---

## RN-027 — As regras consideram a data do evento

### Descrição

Toda validação do domínio deverá utilizar a data de ocorrência do evento como referência principal.

A data de cadastro possui apenas finalidade de auditoria.

---

# 9. Regras Gerais

## RN-028 — Todo evento pode possuir observações

### Descrição

Todos os eventos poderão conter um campo de observação em texto livre.

Esse campo destina-se ao registro de informações relevantes que não possuam modelagem específica no MVP.

---

## RN-029 — Todo evento pode possuir anexos

### Descrição

O domínio permite que eventos possuam fotos associadas.

A forma de armazenamento será definida pela arquitetura da solução.

---

## RN-030 — A linguagem do domínio será Português do Brasil

### Descrição

Todos os conceitos de negócio deverão utilizar Português do Brasil.

Exemplos:

* Animal
* Evento
* Prenhez
* Parto
* Situação
* Estado Reprodutivo

Essa convenção aplica-se ao domínio, Casos de Uso, DTOs, APIs internas e documentação.

---

# 10. Evoluções Previstas

As funcionalidades abaixo fazem parte da visão do produto, porém não compõem o escopo do MVP.

* Vacinação.
* Inseminação.
* Controle sanitário.
* Financeiro completo.
* Estoque.
* Alimentação.
* Produção individual por animal.
* Gestão de funcionários.
* Relatórios avançados.
* Indicadores zootécnicos.

A inclusão dessas funcionalidades deverá respeitar os princípios definidos neste documento.

---

# 11. Revisão da Versão 1.0

## Principais decisões

* O histórico é a fonte da verdade.
* O sistema representa a realidade do produtor.
* Eventos podem ser registrados retroativamente.
* Correções ocorrem por exclusão e novo registro.
* O domínio permanece independente da tecnologia.
* Produção de leite pertence à propriedade.
* Reprodução pertence ao animal.
* O MVP prioriza simplicidade e evolução incremental.

---

## Impacto na implementação

Esta documentação servirá como referência para:

* Casos de Uso.
* Validações do domínio.
* API REST.
* Testes automatizados.
* Modelagem das entidades.
* Arquitetura da solução.

---

## Referências

* DOC-001 — Manifesto
* DOC-002 — Personas
* DOC-003 — Linguagem Ubíqua
* DOC-004 — Modelo de Domínio

---

## Próximo Documento

**DOC-006 — Estados e Transições do Domínio**
