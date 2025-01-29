---
id: 3570
title: 'AWS re:Invent 2013 | Day 2 Keynote with Werner Vogels'
date: 2025-01-29T11:00:41+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=3570
permalink: /opiniao/reinvent-2013-werner-vogels/
history: false

categories:
  - Opinião
---

<img src="/wp-content/uploads/2025/01/reinvent-2013.png" style="vertical-align: middle; border: 0px initial initial;" />

Assisti o keynote de 2013, do Dr Werner Vogels, disponível no youtube:
<a href="https://www.youtube.com/watch?v=Waq8Y6s1Cjs&list=PLtH_rofKo_CNoGdvdnxzQk6ubYhRw6qRA&index=12">Youtube</a>.

E estas são as minhas anotações:

O Dr Werner abre a apresentação falando sobre os parceiros e sobre o ritmo de inovação da aws. Citou o lançamento do sdk javascript, onde podemos invocar apis aws diretamente do browser.

> "Rapid Delivery is in our DNA"


## Work backwards from the Customer
Só construa as funcionalidades que você precisa.

- A primeira coisa que um time faz é escrever um press release, explicando exatamente o que será entregue, em termos simples.
- A segunda é um FAQ, de dez a quinze questões que todo cliente quer saber sobre.
- O passo três, é sobre como será a UX com o produto a ser desenvolvido.
- O passo quatro é começar a escrever o manual de usuário.

Todos esses passos são feitos antes mesmo de começar a escrever a primeira linha de código do produto em si.

## Small, "two pizza" Teams
O objetivo é ter times pequenos o suficiente em que não precisa de reuniões para alinhamentos. É importante entregar a funcionalidade nas mãos do cliente o mais rápido possível, assim já começam a melhorar, lançando primeiro em algumas regiões e posteriormente no resto do mundo.

> "Iterate Based on Customer Feedback"

A aws acredita fortemente na metodologia LEAN, e por isso devemos eliminar desperdícios, que são tudo o que não importa para o consumidor final.

> "The Power of Invention"
Inovação não é somente sobre fazer grandes coisas que ninguém nunca pensou antes, mas também fazer coisas que são realmente importantes ao seu consumidor. Entregando mais ferramentas para que nós os clientes usemos melhor a aws, com:

- Performance
  - Holistic
  - Measure Everything - é importante medir p90 e p99, a única coisa que a média te diz, é que metade dos clientes estão tendo uma performance ok.
  - Measure and Optimize the Full Stack
  - Performance an IO - se você se importa com performance, ter uma performance consistente de IO é muito importante
  - Magnetic Disk is Becoming the New Type
  - Memory is the New Disk
  - Providing Consistent Performance
  - Consistent Performance with DynamoDB
  - Performace is Primary
- Security
  - Fine-Grained Control Over Your Security
  - Fine-Grained Access Control (+ DynamoDB)
  - Access+Encryption
- Reliability
  - Use Multiple Availability Zones
  - Use Multiple Regions
  - Restore Full Stack Application Environments
  - Minimize Recovery Point Objectives
- Cost
  - Never Had the Ability to Set Their Own Price Before
  - Time Insensitive Tasks, Over-clocking Your App
  - Bid Based on the Cost of Interruption (spot)
  - What's next for Computation?
- Scale
  -


## Convidados
- Netflix - Entre a aplicação netflix e a aws, construiram o Netflix platform. Hoje em dia creio que seja o https://github.com/Netflix/mantis, um pouco equivalente ao https://backstage.io
- Instagram - Conseguiram mover dados 20 vezes mais rápido com novos tipos de instâncias.
- Parse - performance consistente com ebs
- airbnb -


## Lançamentos
- Lançou o RDS para bancos postgres
- Lançou a família de instâncias i2
- GSI do dynamodb
- Identity Federation with SAML 2.0
- Redshift Snapshot Copy (multi region)
- Amazon RDS: Cross-Region Read Replicas
- Amazon new C3 Instance Type


