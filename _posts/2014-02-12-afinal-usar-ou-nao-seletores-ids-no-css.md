---
id: 3047
title: Afinal, usar ou não seletores IDs no css ?
date: 2014-02-12T08:00:59+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3047
permalink: /css/afinal-usar-ou-nao-seletores-ids-no-css/
categories:
  - CSS
tags:
  - boas práticas
---
<img src="/wp-content/uploads/2013/05/css.jpg" alt="css" width="800" height="312" class="aligncenter size-full wp-image-3006" srcset="/wp-content/uploads/2013/05/css.jpg 800w, /wp-content/uploads/2013/05/css-300x117.jpg 300w" sizes="(max-width: 800px) 100vw, 800px" />

Eu uso. #prontofalei. Lógico que uso, e vou continuar usando.

<!--more-->

Eu tenho motivos para usar. Identifico os **elementos únicos** no meu documento com ID.

## Eu não uso IDs por performance

É trabalho das engines dos browsers deixarem os seletores rápidos, tanto que hoje em dia usar classes ou id no css, é praticamente a mesma coisa em termos de performance.

Saber disso é um alívio, pois podemos usar classes livremente, mas isso não quer dizer que devemos parar de usar IDs.

## Eu sei usar a cascata

Outro argumento que não faz sentido é dizer que usar seletores IDs faz com que vc brigue por especificidade. Oras, veja bem: usar ID não significa que vc não sabe usar mais nada.

Eu não uso declarações do tipo <var>#menu li</var>, no meu css, mas sim: <var>.menu-item</var>, e ai fica:

``` html
<ul id="menu">
    <li class="menu-item">Item 1</li>
    <li class="menu-item">Item 2</li>
    <li class="menu-item">Item 3</li>
</ul><!-- #menu -->
```

A especificidade que [uso nos meus arquivos css](http://www.maujor.com/tutorial/specificity_wars/specificitywars-05v2.jpg) não passa de 1,1,0 (<var>#id .class</var>). Sendo que a especificidade que mais uso é 0,1,0 (<var>.class</var>) e 0,2,0 (<var>.class .class</var>).

Então usar IDs **com moderação**, com o propósito para o qual foi inventado, não te atrapalha em nada com a cascata ou com a especificidade.

## Referências contra

Encontrei esses 2 links &#8220;famosos&#8221; sobre por que vc não deveria usar seletores ID no teu css.

<http://oli.jp/2011/ids/>

<http://screwlewse.com/2010/07/dont-use-id-selectors-in-css/>

## Referências a favor

E felizmente, também encontrei este outro, dizendo pq vc não deveria se preocupar com isso.

<http://2002-2012.mattwilcox.net/archive/entry/id/1054/>

> They are also, oddly enough, perfectly correct to use as long as they’re only ever one instance of that ID on any given page.
