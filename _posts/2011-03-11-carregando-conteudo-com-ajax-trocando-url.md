---
id: 183
title: Carregando conteudo com ajax, trocando URL
date: 2011-03-11T23:07:15+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=183
permalink: /ajax/carregando-conteudo-com-ajax-trocando-url/
dsq_thread_id:
  - "2101243369"
categories:
  - AJAX
tags:
  - navegação
---
Opa!

Fiz esse <a href="http://forum.imasters.com.br/topic/403171-pagina-dentro-de-div-ajax-problema-ao-atualizar/" target="_blank">script tem um tempo</a>, porém ainda não tinha postado aqui no blog.

Trabalhando com âncoras, resolvi a questão de termos links para &#8216;páginas internas&#8217; de um site, carregado com ajax.

&nbsp;

``` html
<html>
<head>
<script type="text/javascript">
function id( el ){
        return document.getElementById( el );
}
function pega_arq( url ){
        var file = url.split('#');
        return ( file[1] ) ? file[1]+'.html' : 'home.html';
}
function getHTTPObject(){
        if(window.XMLHttpRequest){
                return new XMLHttpRequest();
        }else if(window.ActiveXObject){
                var prefixes = ["MSXML2", "Microsoft", "MSXML", "MSXML3"];
                for(var i = 0; i < prefixes.length; i++){
                        try     {
                                return new ActiveXObject(prefixes[i] + ".XMLHTTP");
                        } catch (e) {}
                }
        }
}
var xmlHttp = getHTTPObject();
function abre( arq ){
        xmlHttp.open("GET", arq,true);
        xmlHttp.onreadystatechange = function(){
                if (xmlHttp.readyState == 4){
                        id('content').innerHTML = xmlHttp.responseText;
                }
        }
        xmlHttp.send( null );
}
window.onload = function(){
        var as = document.getElementsByTagName('a');

        for( var i=0; i<as.length; i++ ){
                as[i].onclick = function(){
                        abre( pega_arq( this.href ) );
                }
        }
        abre( pega_arq( document.location.href ) );
}
</script>
</head>
<body>

        <a href="#contato">Contato</a>
        <a href="#missao-valores">Missão, Valores</a>
        <div id="content">
        </div><!-- /content -->
</body>
</html>
```
