---
id: 1031
title: Só carregar scripts js, se houver suporte a js
date: 2011-05-24T22:30:35+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=1031
permalink: /javascript-puro/so-carregar-scripts-js-se-houver-suporte-js/
dsq_thread_id:
  - "2103277337"
categories:
  - Javascript
---
Uma aplicação interessante de uma função anônima e auto executável
  
<!--more-->

<pre name="code" class="js"></head>
<body>
<script type="text/javascript">
  function load_script( head, path ){
    var script = document.createElement('script'); script.src = path;
    head.appendChild( script );
  }
  (function( head ){
    load_script( head, 'http://ajax.googleapis.com/ajax/libs/jquery/1.6.1/jquery.min.js' );
    load_script( head, 'js/scripts.js' );
  })( document.getElementsByTagName('head')[0] );
</script>
```

Note que faço 2 chamadas à função **load_script**, logo primeiro crio a tag script para o jQuery, e depois crio uma tag script para um arquivo scripts.js local.

Se o visitante estiver com suporte a javascript desabilitado no navegador, ele não irá baixar o script desnecessariamente, pois usamos a própria linguagem para chamar os demais scripts.
  
Pontos importantes a notar, é que essa tag script deve ser posicionada após o fechamento da tag </head>, assim esse elemento já existe no DOM, e a nossa function anônima pode usá-lo.

Passo como argumento para a function autoexecutável, o objeto head, então, não importa qntos scripts eu tenha que incluir, só procuro o objeto **head** uma única vez no DOM.

A função **load_script()** foi criada para reaproveitarmos a rotina.