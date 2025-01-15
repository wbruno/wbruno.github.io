---
id: 1634
title: 'Alterando tamanho de fonte no resize da janela - javascript'
date: 2011-12-07T20:24:59+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1634
permalink: /javascript-puro/alterando-tamanho-de-fonte-resize-da-janela-javascript/
categories:
  - Javascript
---
Boas !

Utilizando hoje o evento window.onresize.

Deixei 800px de largura como sendo a nossa largura inicial. Apartir dela, vou aumentar a fonte do documento, conforme a janela adquira mais largura, e caso seja menor que 800px; volto ao meu inicial&#8230;

<!--more-->

``` html
<html>
<head>
<script type="text/javascript">
window.onload = function(){
  document.getElementById('result').innerHTML = document.body.offsetWidth;

}
window.onresize = function(){
  document.getElementById('result').innerHTML = document.body.offsetWidth;

  var bodyWidth = document.body.offsetWidth;
  if( bodyWidth>800 )
    fs = ( bodyWidth-800 )/10;
  else
    fs = 0;

  document.getElementsByTagName('h1')[0].style.fontSize = (fs+20)+'px';
  document.body.style.fontSize = (fs+12)+'px';
}
</script>
<style type="text/css">
body { font-size: 12px; }
h1 { font-size: 20px; }
</style>
</head>
<body>
  <h1>Algum texto aqui</h1>
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse a leo dolor. Etiam fermentum mi metus,
  vel dignissim dui. Sed non adipiscing risus. Suspendisse sed massa ac ipsum consequat ornare. Donec pretium
  urna at ipsum adipiscing ut sagittis ligula malesuada. Mauris nec quam fringilla massa hendrerit consequat.
  Aenean congue porta consectetur. In pellentesque auctor elementum. Curabitur eleifend, ante eget fringilla
  tempus, metus sem viverra enim, eu ullamcorper urna neque non ante. In sagittis malesuada faucibus. Nam nec
  malesuada nulla. Suspendisse semper suscipit lacinia. Etiam commodo tellus nec eros auctor ac malesuada arcu
  rutrum. Quisque tortor sapien, volutpat at consequat sed, dapibus tincidunt libero. Quisque malesuada est at
  erat suscipit sit amet suscipit dui blandit.</p>

  <p>Quisque in nulla hendrerit arcu facilisis hendrerit vitae sit amet massa. Suspendisse fermentum ligula
  congue sem fringilla sit amet pulvinar sem iaculis. Donec turpis orci, tempor sit amet sodales eu, cursus a
  nunc. Nulla sagittis velit id lorem dignissim porta. In congue ipsum ut ligula elementum suscipit nec sed ante.
  Cras felis eros, faucibus quis malesuada non, aliquet sed risus. Nullam pellentesque dui ligula. Lorem ipsum
  dolor sit amet, consectetur adipiscing elit. Sed neque metus, posuere porta luctus eget, molestie non lectus. </p>

  <div id="result"></div>
</body>
</html>
```

## <a href="/scripts/fontsize.html" target="_blank">Demonstração</a>
