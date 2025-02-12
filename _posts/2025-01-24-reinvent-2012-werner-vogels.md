---
id: 3569
title: '2012 re:Invent Day 2 Keynote: Werner Vogels'
date: 2025-01-24T11:00:41+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=3569
permalink: /opiniao/reinvent-2012-werner-vogels/
history: false

categories:
  - Opinião
---

<img src="/wp-content/uploads/2025/01/reinvent-2012.png" style="vertical-align: middle; border: 0px initial initial;" />

Assisti o keynote de 2012, do Dr Werner Vogels, disponível no 
<a href="https://www.youtube.com/watch?v=PW1lhU8n5So&list=PLtH_rofKo_CNoGdvdnxzQk6ubYhRw6qRA&index=13">Youtube</a>.

E estas são as minhas anotações:

O Dr Werner abre a apresentação citando outra que ele fez em 2007, onde os maiores benefícios da cloud são:
- Lowers Cost
- Increases Agility
- Removes the "Heavy Lifiting"
- Foudation for 21th Century Architectures

No "Old World", existiam diversas restrições, como hardware. No novo mundo, podemos construir arquiteturas que não estão mais restringidas, a não ser pela velocidade da luz.
Se provisionarmos para picos, sem elasticidade (servidores físicos), a amazon teria ociosidade em ~39 a 76% do tempo.

21st Century Architectures, são:
- Secure
- Scalable
- Fault tolerant
- High performance
- Cost effective

> "Acredite em mim, eu abracei um monte de servidores na minha vida, e eles não te abraçam de volta"

Em 2010 e 2011, eles desligaram os últimos servidores físicos e o gráfico de provisionamento agora acompanha o uso real, com muito menos desperdício.

Agora, construimos arquiteturas focando no negócio e não mais em recursos.
Os requisitos mudam e isso nos aborrece, porém esse é o mundo real, devemos projetar sabendo que vai mudar, e ao não precisar mais nos preocupar com os recursos, usamos a cloud para atender o negócio.
Devemos abandonar arquiteturas centradas em data centers, focada em recursos. E fazer arquiteturas focadas no negócio.
Onde antes tinhamos restrições de recursos, agora com cloud temos recursos programáveis, usando capacidade ilimitada na aws.

## Commandments of 21st Century Architectures
- Controllable
  - Decomposable into small, loosely couple, stateless building blocks
  - Automate your application and processes
  - Let business levers control the system
  - Architect with cost in mind
  - Pequenas unidades de escala, unidades com tolerância a falha
- Resilient
  - Protecting your customers is the first priority
  - In production, deploy at least two availability zones
  - Integrate security into your application from the ground up
  - Build, test, integrate and deploy continuously
  - Don't think in single failures
  - Don't thread failure as an exception
- Adaptative
  - Assume nothing
  - Use late biding
- Data Driven
  - Instrument everything, all the time
  - Inspect the whole distribution
  - Put everything in logs
  - Thou shalt turn off the lights

- > "ec2 instances are not servers"
- > "everything fails all the time"

Houve o lançamento do AWS Data Pipeline, que posteriormente foi descontinuado e já está em modo manutenção nos dias de hoje (2025).
