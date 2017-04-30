---
id: 493
title: Não use jQuery ! Não aprenda qualquer FrameWork antes de..
date: 2011-04-04T08:24:00+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=493
permalink: /opiniao/nao-jquery-nao-aprenda-qualquer-framework-antes-de/
dsq_thread_id:
  - "2101221955"
categories:
  - Opinião
tags:
  - framework
---
**antes de..** conhecer um **mínimo da linguagem base** em que esse FW foi escrito.

É por isso que existem tantos desenvolvedores se enrolando hoje em dia. Tentam usar bibliotecas, frameworks e ajax, antes de aprender o básico.

[<img src="/wp-content/uploads/2011/04/elephpant-elephant-php-logo_big.png" alt="" title="elephpant-elephant-php-logo_big" width="150" height="96" class="alignright size-full wp-image-496" />](/wp-content/uploads/2011/04/elephpant-elephant-php-logo_big.png)

Aprender CodeIgniter, Kohana, CakePHP, Smarty&#8230;antes de aprender php é loucura, certo? Ninguém faz curso de ZendFW, sem **nunca**, ter programado php. Primeiro aprende php, e depois vai para um FW. Então por que inverter os papeis com JavaScript ?

<!--more-->

Okay, a curva de aprendizado do jQuery[assim como dos demais fws] é menor, porém e quando aparece um problema ?

[<img src="/wp-content/uploads/2011/04/JQuery_logo_color_onwhite.png" alt="" title="JQuery_logo_color_onwhite" width="229" height="200" class="alignleft size-full wp-image-505" />](/wp-content/uploads/2011/04/JQuery_logo_color_onwhite.png)

Aí, aquele desenvolvedor, que optou por começar com o framwork, sem antes passar pela linguagem base, começa a ter dúvidas básicas de programação. O FW não resolve tudo para ele.

Só vai facilitar o trabalho, se ele não se enrolar com os conceitos fundamentais.

Já vi gente pedindo <u>plugin</u> jQuery _para descobrir o que está na url_. Veja, ele não queria e nem precisava fazer um parser da querystring, ele só precisava saber o que estava lá. Não sabia da existência do **documen.location**, e das diversas propriedades desse objeto.

Outro cara ainda, não queria usar o **document.createElement()**, ele insistia em _querer fazer com jQuery_! Okay, <a href="http://blogs.microsoft.co.il/blogs/basil/archive/2008/08/21/jquery-create-jquery-plug-in-to-create-elements.aspx" target="_blank">existe plugin pra isso</a>!! Mas pra quê ? O método nativo da linguagem já é tão bom! Vamos deixar para o FW, o que <u>deve ser</u> do FW. Ficar inchando nosso documento de plugins só vai detonar o tráfego. Usar plugins e FWs, onde não é necessário, só vai deixar nossa aplicação mais lenta!

Outro caso: eu respondi a dúvida dele, que era super simples, usando apenas js, eram 3 ou 4 linhas de código. Ele testou, disse que funcionou, e depois pediu para ver _como ficaria aquilo em jQuery_. Era idiota reescrever 4 linhas de js, usando o FW, e nem dava! Mas para o cara:

> **JavaScript**, estava <u>ultrapassado</u>, e ele pretendia fazer _da forma moderna_.

O mesmo ocorreu com AJAX. A dúvida estava resolvida, aí o cara pediu para _ver como ficaria em AJAX_! E era tudo apenas javascript puro, não havia o menor motivo para _ir no servidor e voltar_.

[<img src="/wp-content/uploads/2011/04/ajax-logo2.jpg" alt="" title="ajax-logo" width="200" height="98" class="alignright size-full wp-image-513" />](/wp-content/uploads/2011/04/ajax-logo2.jpg)

Nesse momento começa a sugir uma confusão de papeis. Gente achando que AJAX é uma linguagem, que precisa enfiar jQuery em tudo&#8230;

Já vi tópico começar &#8216;sobre AJAX&#8217;, e terminar apenas com php puro! O cara queria meter uma requisição assincrona onde não precisava. Completa inversão de valores, e pura falta de conhecimento.

Da mesma forma sou <u>contra</u>, os caras que começam a aprender linguagens server-side, sem antes terem algum contato com HTML! Isso é básico. Programando web, precisamos de HTML, é a linguagem padrão que vai possibilitar todo o resto. O teu php, asp, java.. vai gerar HTML mais cedo ou mais tarde.

Daí, começam a surgir dúvidas ridículas. O cara vai fazer uma listagem de produtos para uma loja virtual, e não sabe como colocar um produto do lado do outro. Isso é porque ele não sabe HTML, quem dirá CSS! Sem entrar no mérito da divisão de trabalho, FrontEnd, BackEnd.. ao menos um pouco da linguagem do outro, era bacana.

Em agências pequenas, ou como freelancer, muitas vezes o mesmo profissional faz ambos. /(Front|Back)End/

Alguns passos são importantes, e devem ser respeitados. Comece do básico, evolua, e aí sim vá para o além.

Antes de tudo, você recebe aulas de **Lógica de Programação** e **Programação Básica**, certo ? Deveria ser assim, mas me assusta a quantidade de programadores que vejo no mercado, que não possuem essa base na formação.

Pra mim:

> **todo programador**, deveria, **obrigatoriamente**, estudar alguma linguagem de programação de **baixo nível**.

Alguns hoje em dia, não conhecem a diferença, ou nem sabem que existe isso!

Não, não estou sendo arcaico. Estou sendo realista. O conhecimento adquirido ao fazer algo em Assembly por exemplo, é extraordinário. Se todos passassem por essa experiência, não teríamos tanto lixo sendo criado. Não precisa se tornar sênior, nem ser ótimo em HTML e CSS, nem defender tese de mestrado em lógica&#8230;

Mas coisas como tipagem, declaração de variáveis, coletor de lixo, escopo.. faltam a vários programadores php e js que conheço. Vejo pessoas no fórum **declarando** uma function, _achando_ que ela será executada, só com isso. Sem ele fazer uma chamada a ela.

[<img src="/wp-content/uploads/2011/04/frameworks.jpg" alt="" title="frameworks" width="300" height="230" class="alignright size-full wp-image-521" />](/wp-content/uploads/2011/04/frameworks.jpg)

Ponto importante é **não ser dependente** do Framework. Okay, vc sabe fazer com ele. Mas e sem ?

E se a sua empresa resolver mudar de paradigma, ou você mudar de trabalho, e lá usarem outros, ou nenhum? como fica?

Você novamente, vai gastar um bom tempo, reaprendendo outra ferramenta, que poderia ser muito menor se você, tivesse alguma idéia, do **como**, essas ferramentas fazem o que fazem.

A **Inversão de Controle**, pode ser a tua amiga. Conheço todos os &#8216;bons motivos&#8217; de se usar um FrameWork, o meu ponto é: Não comece por ele. Vá evoluindo, e aprendendo a base.
