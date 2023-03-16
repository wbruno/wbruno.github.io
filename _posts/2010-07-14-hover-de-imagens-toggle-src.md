---
id: 61
title: hover de imagens toggle src
date: 2010-07-14T12:01:32+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=61
permalink: /javascript-puro/hover-de-imagens-toggle-src/
categories:
  - Javascript
---
``` html
<html>
<head>
<script type="text/javascript">
window.onload = function()
{
        var normal = '';
        toggle_src( id('a1') );
        toggle_src( id('a2') );
}
function id( el ){
        return document.getElementById( el );
}
function toggle_src( el )
{
        el.onmouseover = function(){
                normal = this.src;
                this.src = this.lowsrc;
        }
        el.onmouseout = function(){
                this.src = normal;
        }
}
</script>
</head>

        <a href="#"><img src="normal-home.jpg" width="75" id="a1" height="58" alt="Botão para a Página Inicial" lowsrc="hover-home.jpg" /></a>
        <a href="#"><img src="normal-contato.jpg" width="75" id="a2" height="58" alt="Botão para a Página Inicial" lowsrc="hover-contato.jpg" /></a>
</body>
</html>
```