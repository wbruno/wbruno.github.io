---
id: 324
title: Div centralizada vertical/horizontal, e fixa com rolagem da janela
date: 2011-03-23T09:01:07+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=324
permalink: /javascript-puro/div-centralizada-verticalhorizontal-fixa-rolagem-da-janela/
dsq_thread_id:
  - "2102136911"
categories:
  - Javascript
---
Hehe, salve salve!!

Acabei de fazer um post: [Div centralizada vertical/horizontal, e fixa com resize da janela](http://www.wbruno.com.br/2011/03/23/div-centralizada-verticalhorizontal-fixa-resize-janela/), mas ai vi que faltava uma coisa nele:

A div se movimentar junto com a rolagem da janela(tecnicamente), ou seja, a DIV ficar fixa(aparentemente pro usuario).
  
Aquela coisa chata de propagandas, em que vc vai rolando o site, e tem um treco na frente.. que não sai do meio da tela.
  
<!--more-->


  
Apesar de chato pro usuário, ajuda bastante os desenvolvedores a divulgar informações.
  
Pequena alteração no outro script:

Onde era somente:

``` js
window.onload = function(){
  calcMarginTop();
}
```

Agora deve ficar assim:

``` js
var marginTopoInicial;//criando variavel de escopo global
window.onload = function(){
  calcMarginTop();
  marginTopoInicial = parseInt( getMarginTop( id('main') ) );//recuperando o marginTop inicial
}
window.onscroll = function(){
  id('main').style.marginTop = marginTopoInicial+window.pageYOffset+'px';//levando em conta o scroll
}
```

=) por enqnto é isso.

<a href="http://www.wbruno.com.br/scripts/div-centralizada-fixed.html" target="_blank">Demonstração</a>