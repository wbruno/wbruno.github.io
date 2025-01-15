---
id: 216
title: Princípio de Menu em Abas
date: 2011-03-12T00:36:05+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=216
permalink: /javascript-puro/principio-de-menu-em-abas/
dsq_thread_id:
  - "2102923984"
categories:
  - Javascript
---

``` html
<html>
<head>
        <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
<script type="text/javascript">
function id( el ){
        return document.getElementById( el );
}
function hide_all(){
        var divs = id('content').getElementsByTagName('div');
        for( var i=0; i<divs.length; i++ )
        {
                divs[i].style.display = 'none';
        }
}
/* http://www.javascriptkit.com/jsref/event.shtml */
function disablelink( e ){
        var evt = window.event || e
        if (evt.preventDefault) //supports preventDefault?
                evt.preventDefault()
        else //IE browser
                return false
}
window.onload = function(){
        hide_all();
        var as = id('content').getElementsByTagName('a');
        for( var i=0; i<as.length; i++ )
        {
                as[i].onclick = function( e ){
                        hide_all();
                        var id_el = this.href.split('#')

                        id( id_el[1] ).style.display = 'block';
                        return disablelink( e );
                }
        }
}
</script>
</head>
<body>
        <div id="content">
                <a href="#historia">História</a><br />
                <div id="historia">Conteudo da História</div>

                <a href="#geografia">Geografia</a><br />
                <div id="geografia">Conteudo da Geografia</div>

                <a href="#matematica">Matemática</a><br />
                <div id="matematica">Conteudo da Matemática</div>

        </div><!-- /content -->
</body>
</html>
```
