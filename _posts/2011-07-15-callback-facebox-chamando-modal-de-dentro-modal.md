---
id: 1145
title: 'CallBack facebox - chamando o modal de dentro do modal'
date: 2011-07-15T07:00:17+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1145
permalink: /jquery/callback-facebox-chamando-modal-de-dentro-modal/
dsq_thread_id:
  - "2104696053"
categories:
  - jQuery
tags:
  - modal
---
Galera está tendo bastante dificuldade com isso hoje em dia.

> Tenho um modal, que abre pegando um conteúdo com ajax ou não.

O ponto é que os plugins de modal(ou a maioria deles), e também o facebox que é o caso que vou demonstrar agora, reescrevem o conteúdo com js, então perdemos qualquer função atrelada que tínhamos.

<!--more-->

## Com &#8220;Defeito&#8221;

<a href="/scripts/facebox1.html" target="_blank">Janela Modal FaceBox</a>

``` html
<html>
<head>
  <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js"></script>
  <script type="text/javascript" src="src/facebox.js"></script>

  <link href="src/facebox.css" media="screen" rel="stylesheet" type="text/css" />

  <script type="text/javascript">
  $(document).ready(function(){
    $('a[rel*=facebox]').facebox({
      loadingImage : 'src/loading.gif',
      closeImage   : 'src/closelabel.png'
    });
  });
  </script>
  <style type="text/css">
  .modal { display: none; }
  </style>
</head>
<body>
  <a href="#modal" rel="facebox">Abrir Modal</a>

  <div id="modal" class="modal">
    Modal <a href="#modal2" rel="facebox">Abrir outro modal</a>
  </div><!-- /modal -->
  <div id="modal2" class="modal">
    Segundo Modal.
  </div><!-- /modal -->
</body>
</html>
```

Note que clicando no link do segundo modal, oque acontece é que a URL muda para **#modal2**, e o comportamento de abrir outro modal não é feito.

Por causa do que eu disse, do conteúdo do modal ter sido reescrito com js, então o link:

``` html
<a href="#modal2" rel="facebox">Abrir outro modal</a>
```
não teve o comportamento atrelado.

Precisamos, logo depois de abrir o primeiro modal, colocar esse comportamento nos links lá.

Uma forma elegante de fazer isso, é no callback do próprio modal, rodarmos a rotina:

``` js
$(document).bind('afterReveal.facebox', function(){
      $('#facebox .content a').facebox({
        loadingImage : 'src/loading.gif',
        closeImage   : 'src/closelabel.png'
      });
    });
```

Não fiz nada de anormal, ou super.

Apenas <a href="http://defunkt.io/facebox/" target="_blank">li a documentação</a>, e entendendo o motivo de ter falhado, resolvi.

## <a href="/scripts/facebox2.html" target="blank">Demonstração</a>
