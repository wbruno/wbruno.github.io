---
id: 1760
title: Alterar dimensões de embed do youtube com javascript
date: 2012-01-25T13:23:24+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1760
permalink: /javascript-puro/alterar-dimensoes-de-embed-youtube-javascript/
categories:
  - Javascript
tags:
  - iframe
  - youtube
---
Repositório, para deixar arquivado aqui.
  
Veja que ao clicar em cada botão, o tamanho do vídeo se altera.

``` html
<html>
<head>
<style type="text/css">
* { margin: 0; padding: 0; }
html, body { height: 100%; }
</style>
<script type="text/javascript">
function sizeIframe( w, h )
{
  document.getElementById('yt').width = w;
  document.getElementById('yt').height = h;
}
window.onload = function(){
  sizeIframe( document.body.offsetWidth, document.body.offsetHeight-30 );
}
</script>
</head>
<body>
  <iframe width="420" height="315" src="http://www.youtube.com/embed/tvaPMNq4Ey0" frameborder="0" allowfullscreen id="yt"></iframe>
  
  <input type="button" name="mudar" value="600x480" onclick="sizeIframe( 600, 480 )" />
  <input type="button" name="mudar" value="600x480" onclick="sizeIframe( 420, 315 )" />
  <input type="button" name="mudar" value="300x240" onclick="sizeIframe( 300, 240 )" />
</body>
</html>
```

É isso. Me diga se vc usar.