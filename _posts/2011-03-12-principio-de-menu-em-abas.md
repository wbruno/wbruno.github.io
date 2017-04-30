---
id: 216
title: Princípio de Menu em Abas
date: 2011-03-12T00:36:05+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=216
permalink: /javascript-puro/principio-de-menu-em-abas/
dsq_thread_id:
  - "2102923984"
categories:
  - Javascript
---
<pre class="javascript">&lt;html&gt;
&lt;head&gt;
        &lt;meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" /&gt;
&lt;script type="text/javascript"&gt;
function id( el ){
        return document.getElementById( el );
}
function hide_all(){
        var divs = id('content').getElementsByTagName('div');
        for( var i=0; i&lt;divs.length; i++ )
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
        for( var i=0; i&lt;as.length; i++ )
        {
                as[i].onclick = function( e ){
                        hide_all();
                        var id_el = this.href.split('#')
                       
                        id( id_el[1] ).style.display = 'block';                
                        return disablelink( e );
                }
        }
}
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
        &lt;div id="content"&gt;
                &lt;a href="#historia"&gt;História&lt;/a&gt;&lt;br /&gt;
                &lt;div id="historia"&gt;Conteudo da História&lt;/div&gt;
               
                &lt;a href="#geografia"&gt;Geografia&lt;/a&gt;&lt;br /&gt;
                &lt;div id="geografia"&gt;Conteudo da Geografia&lt;/div&gt;
               
                &lt;a href="#matematica"&gt;Matemática&lt;/a&gt;&lt;br /&gt;
                &lt;div id="matematica"&gt;Conteudo da Matemática&lt;/div&gt;

        &lt;/div&gt;&lt;!-- /content --&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>