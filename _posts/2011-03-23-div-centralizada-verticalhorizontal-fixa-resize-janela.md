---
id: 319
title: Div centralizada vertical/horizontal, e fixa com resize da janela
date: 2011-03-23T08:21:09+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=319
permalink: /javascript-puro/div-centralizada-verticalhorizontal-fixa-resize-janela/
dsq_thread_id:
  - "2101313241"
categories:
  - Javascript
---
Salve!!

Mais um script da série de scripts perdidos que já <a href="http://forum.imasters.com.br/topic/422036-centralizado-vertical-e-horinzontal-apenas-no-safari/page__view__findpost__p__1664388" target="_blank">desenvolvi para o fórum iMasters</a>, e só encontrei agora.

O script tem um css simples para centralizar uma DIV horizontalmente e verticalmente.
  
Porém, o problema disso, é que se a área da viewport do browser, for menor (menos alta ou menos larga), que as dimensões da tua DIV, essa DIV começa a &#8216;se esconder&#8217;, para dentro do overflow da viewport.

Para resolver essa questão, disparei no evento onresize da janela, uma rotina javascript que calcula as margens, se essas forem menores que o necessário, e então reposiciona a DIV alí no centro.

<!--more-->

``` html
<html>
<head>
<script type="text/javascript">
function id( el ){
  return document.getElementById( el );
}
window.onload = function(){
  calcMarginTop();
}
window.onresize = function(){
  calcMarginTop();
}
function calcMarginTop()
{
  var main = id('main');
  var marginTopo = parseInt( getMarginTop( main ) );
  var marginBaixo = parseInt( getMarginBottom( main ) );


  if( main.offsetTop < -1 )
    main.style.marginTop = '-'+( parseInt( main.offsetTop ) - marginTopo )+'px';
  else if( marginTopo!=marginBaixo )
  main.style.marginTop = '-248px';
}
function getMarginTop( el )
{
  if( window.getComputedStyle )
    return document.defaultView.getComputedStyle(el, null).marginTop;
  else if( el.currentStyle )
    return el.currentStyle['marginTop'];
}
function getMarginBottom( el )
{
  if( window.getComputedStyle )
    return document.defaultView.getComputedStyle(el, null).marginBottom;
  else if( el.currentStyle )
    return el.currentStyle['marginBottom'];
}
</script>
<style type="text/css">
* { margin: 0; padding: 0; }
#main {
  border: 1px solid #000;
  height: 500px;
  width: 500px;
  top: 50%;
  left: 50%;
  margin-top: -250px;
  margin-left: -250px;
  position: absolute;
}
</style>
</head>
<body>
  <div id="main">

  </div><!-- /main -->
</body>
</html>
```

Bom, é isso. Comentem! Gostaria de ouvir sugestões.