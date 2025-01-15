---
id: 417
title: O que é ajax, e o que não é?
date: 2011-04-08T07:01:42+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=417
permalink: /ajax/o-que-e-ajax-e-o-que-nao-e/
dsq_thread_id:
  - "2102307737"
categories:
  - AJAX
---
Do começo e com as minhas palavras:

<h2 style="display: inline;">
  AJAX
</h2>

<p style="display: inline;">
  é mais simples do que parece. A grosso modo, não temos refresh(próprio das requisições HTTP comuns) para <strong>trazer respostas do servidor</strong>. O ponto importante a notar aqui, é que enviamos informações, e teremos um retorno(mesmo funcionamento de uma requisição HTTP).
</p>

[<img src="/wp-content/uploads/2011/04/ajax-222x300.jpg" alt="" title="ajax" width="222" height="300" class="alignright size-medium wp-image-702" srcset="/wp-content/uploads/2011/04/ajax-222x300.jpg 222w, /wp-content/uploads/2011/04/ajax.jpg 300w" sizes="(max-width: 222px) 100vw, 222px" />](/wp-content/uploads/2011/04/ajax.jpg)Esse retorno, pode vir &#8216;formatado&#8217; (jSON, XML, HTML&#8230;), mas ainda assim **é apenas** <u>texto puro</u>. Não é retornado por exemplo &#8216;um array php, ou uma variavel&#8217;, mas sim um <u>texto puro</u>(o output dessa variavel, desse array&#8230;).

<h5 style="font-weight: normal;">
  Alguns conceitos e definições:
</h5>

**JavaScript** é uma <u>linguagem de script</u> client-side;

**FrameWork**s são um conjuntos &#8216;de códigos&#8217; que devem facilitar o desenvolvimento de rotinas especifícas ou aplicações completas;

**jQuery** É apenas um FrameWork(dentre muitos) escrito sob a linguagem JavaScript.

**AJAX** É a reunião de várias tecnologias, formando uma metodologia de desenvolvimento.

**DOM** é uma especificação que não depende de linguagem nem plataforma. Um padrão de acesso aos documentos, e por consequência aos elementos dele.

<!--more-->



Vou me ater ao nosso contexto, conheço as definições completas de cada um dos termos.

Antes de falar sobre _Onde usar e onde não usar AJAX?_, alguns desenvolvedores precisam entender **o que é ajax, e o que não é**.

Enquanto ainda estamos manipulando o DOM, não estamos lidando com ajax ainda. Se podemos trazer o conteúdo já na carga do documento, então devemos fazer da forma simples.

> <em style="font-size: 20px;">Leia a palavra &#8216;ajax&#8217; como &#8216;requisição&#8217;.</em>

Se tem &#8216;requisições&#8217; na jogada então <u>talvez</u>, você tenha ajax. Se não tem, e nem precisa requisitar nada ao servidor, então não temos ajax.

Precisa de alguma informação que **só** a tua linguagem server-side, pode dar ? Necessita disso sem um refresh da tela? Se não puder trazer essa informação já na tela, ai sim, você precisa de ajax.

[<img src="/wp-content/uploads/2011/04/ajax-logo2.jpg" alt="" title="ajax-logo" width="200" height="98" class="alignleft size-full wp-image-513" />](/wp-content/uploads/2011/04/ajax-logo2.jpg)Não existe uma &#8216;forma ajax&#8217; de resolver. O correto é analisar se vale a pena usar ou não, se era necessário, se encaixa no teu contexto&#8230;

Ajax não são efeitos. Não é qualquer coisa que não faça refresh. Ajax não é a solução para tudo.. Ajax não substitui o flash. Ajax não envia arquivos. Ajax sozinho não faz barras de loading&#8230;. Ajax não é jQuery. jQuery não é Ajax. Não é uma linguagem, nem sub-linguagem (ouvi essa no forum). Não é cálculo entre inputs'(se não depender de informações de um banco de dados por exemplo). Não é Drag And Drop. Não faz slideshow&#8230;

Use ajax onde você não puder fazer da forma convencional, e ainda assim, deixe funcionando, mesmo que o usuário não tenha suporte a javascript.

Ajax pode ser usado para enriquecer e muito a experiência do usuário. Ajax é melhorar a usabilidade da sua aplicação. Ajax é não obrigar o cliente, a descarregar todo um conteúdo estático, que não ia sofrer alteração, apenas para enviar e receber uma resposta simples do servidor. Ajax é uma forma de interagir mais, de tornar as tuas páginas web, mais próximas das aplicações desktop. Ajax é economia de banda se bem usado. Ajax é composto por várias tecnologias. Ajax é um conceito.

Na verdade, no fundo no fundo, ajax é fazer uma requisição assíncrona ou não. E dela trazer um retorno, <u>sem depender</u> do refresh da tela. É isso. Mas muitos usam de forma errada. Abusam onde não deveriam, confundem&#8230;

E de novo, começam a querer usar, sem conhecer as linguagens base pelas quais todo o processo é feito.

Ajax é perigoso. Se mal usado, pode comprometer todo o site, toda a aplicação, deixar tudo mais lento, detonar a banda, expor o sistema&#8230; Não é culpa da linguagem javascript, mas sim da forma com que estão fazendo os sistemas hoje em dia. É client-side galera !! Acordem!

Possui vulnerabilidades por estar exposto, tudo porcamente programado, é vulnerável. AJAX bem feito e bem usado, só trás benefícios. A antítese também é verdadeira:

> _AJAX mal feito e mal usado, só trás problemas!_

AJAX pode ser muito melhor e muito mais. Entretanto, é preciso ter bom senso de saber os locais certos, onde se deve ou não aplicar.
