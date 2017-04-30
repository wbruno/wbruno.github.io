---
id: 167
title: 'Principio de slideshow &#8211; setTimeout recursivo'
date: 2011-03-11T21:11:32+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=167
permalink: /javascript-puro/principio-de-slideshow-settimeout-recursivo/
dsq_thread_id:
  - "2101117727"
categories:
  - Javascript
tags:
  - slideshow
---
slideshow simples, apenas trocando o src de uma tag img com javascript puro.

<pre name="code" class="javascript">&lt;script type="text/javascript">
        var x = new Array('images/1.jpg','images/2.jpg');
        var total = x.length-1;

        var pos = 0;
        function mudar()
        {
                document.getElementById('fig1').src = x[pos];
                window.setTimeout( mudar, 500 );


                pos++;
                if( pos>total ) pos = 0;
        }
        window.onload = function(){
                mudar();
        }
&lt;/script>
&lt;img src="images/2.jpg" alt="" id="fig1" />
</pre>

Veja a <a href="http://www.wbruno.com.br/scripts/principio-slideshow.html" target="_blank">demo em funcionamento</a>