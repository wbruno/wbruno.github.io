---
id: 2841
title: 'Column.GS - Um sistema de grid css 960 com significado e para FrontEnds'
date: 2012-11-17T12:56:10+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2841
permalink: /css/column-gs-um-sistema-de-grid-css-960-com-significado-e-para-frontends/
dsq_thread_id:
  - "2104088517"
categories:
  - CSS
---
Criei esse [sistema de GRID css de 12 colunas](https://wbruno.com.br/css/column-gs-um-sistema-de-grid-css-960-com-significado-e-para-frontends/), para atender uma necessidade que tive durante o recorte de páginas de um site.

<!--more-->



O sistema nasceu para ser diferente dos demais. Se aproveitando do expertise de cada um deles, e mesclando o que eu achei de melhor.

Peguei o PSD do projeto 960.gs e incorporei no meu projeto no [github](https://github.com/wbruno/column.gs "Column.GS no github").

Já venho usando a alguns meses, e o sistema de grid me atende bem. Faço sites de todos os tipos.

Sem sujar o html, posicionamento elementos corretamente(com floats e margins), sem uso de elementos desnecessários e com classes intuitivas.

## Strudel Folhadinho

Este site de [venda de strudels em são paulo](http://strudelfolhadinho.com.br/ "Venda de Strudel de Maçã em São Paulo"), é o meu primeiro usando o column.gs até para fazer a base do responsivo.

[<img src="/wp-content/uploads/2012/11/311325_175002752638934_124201893_n.jpeg" alt="" title="311325_175002752638934_124201893_n" width="960" height="480" class="aligncenter size-full wp-image-2842" srcset="/wp-content/uploads/2012/11/311325_175002752638934_124201893_n.jpeg 960w, /wp-content/uploads/2012/11/311325_175002752638934_124201893_n-300x150.jpeg 300w" sizes="(max-width: 960px) 100vw, 960px" />](/wp-content/uploads/2012/11/311325_175002752638934_124201893_n.jpeg)

## Feito para FrontEnds

Se você tem um sistema grande, e precisa de um layout &#8220;pre moldado&#8221;, então eu indico usar o Twitter Bootstrap. Mas se você tb não gosta de posicionar elementos com padding(assim como o 960.gs), então o column.gs é ideal para você.

São classes simples como: &#8220;coluna-um-terço&#8221;, &#8220;columa-metade&#8221;, &#8220;coluna-dois-terços&#8221;..

E toda a mágica será feita. O poder deve ficar com o desenvolvedor, e não ser limitado pelo framework.

A pequena inversão de controle que existe aqui, é: &#8220;não declare larguras no teu css&#8221;. Deixe os <var>width</var>s a cargo do column.gs. Todos eles.

### Boas práticas

-> Não estilize no css do teu projeto, as classes da grid. Elas devem aparecer unicamente no html, e no css da grid.

-> Ao usar 2 colunas(<var>column-half</var>), lembre-se de não usar espaçamentos. Mas deixar isso pelo ganho natural do <var>float: left</var> e <var>float: right</var>.

O mesmo vale para 3, 4 colunas e demais. Coloque como <var>fright</var> a última coluna da direita, e a na esquerda anterior a esta, não coloque margin.

## Column.GS no github

[Subi para o github](https://github.com/wbruno/column.gs "Column.GS no github") para que você pudesse me ajudar. Abra issues, use.

Me diga oque vc acha. Faz o seu fork lá.

=) Comente aqui! envie seu pull request.
