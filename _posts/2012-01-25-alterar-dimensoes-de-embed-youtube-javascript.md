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

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;style type="text/css">
* { margin: 0; padding: 0; }
html, body { height: 100%; }
&lt;/style>
&lt;script type="text/javascript">
function sizeIframe( w, h )
{
	document.getElementById('yt').width = w;
	document.getElementById('yt').height = h;
}
window.onload = function(){
	sizeIframe( document.body.offsetWidth, document.body.offsetHeight-30 );
}
&lt;/script>
&lt;/head>
&lt;body>
	&lt;iframe width="420" height="315" src="http://www.youtube.com/embed/tvaPMNq4Ey0" frameborder="0" allowfullscreen id="yt">&lt;/iframe>
	
	&lt;input type="button" name="mudar" value="600x480" onclick="sizeIframe( 600, 480 )" />
	&lt;input type="button" name="mudar" value="600x480" onclick="sizeIframe( 420, 315 )" />
	&lt;input type="button" name="mudar" value="300x240" onclick="sizeIframe( 300, 240 )" />
&lt;/body>
&lt;/html>
</pre>

É isso. Me diga se vc usar.