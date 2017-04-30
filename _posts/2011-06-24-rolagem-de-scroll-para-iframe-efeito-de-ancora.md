---
id: 1121
title: 'Rolagem de scroll indo para um iframe &#8211; efeito de âncora'
date: 2011-06-24T07:00:27+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1121
permalink: /javascript-puro/rolagem-de-scroll-para-iframe-efeito-de-ancora/
dsq_thread_id:
  - "2106749189"
categories:
  - Javascript
tags:
  - iframe
---
Boas galera!!

Respondendo uma dúvida no iMasters, vi que não é possível usarmos âncoras HTML com iframes(pelo menos eu não consegui) .
  
O menu tá lá em cima, e o iframe no meio do conteudo, escondido pela rolagem.
  
<!--more-->


  
isso aqui:

<pre name="code" class="html">&lt;a href="http://www.google.com.br/#externo" target="externo" id="google">google&lt;/a>
        
        &lt;iframe src="" name="externo" id="externo" width="1000px">&lt;/iframe></pre>

infelizmente não funciona.

Logo, a próxima solução que pensei, foi usar javascript para tal:

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;script type="text/javascript">
window.onload = function(){
        document.getElementById('google').onclick = function(){
        
                window.document.body.scrollTop = document.getElementById('externo').offsetTop;
        
        }
}       
&lt;/script>
&lt;/head>
&lt;body>
        &lt;a href="http://www.google.com.br/" target="externo" id="google">google&lt;/a>
        &lt;div id="espaco">
                &lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />
                &lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />
                &lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />
                &lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />
                &lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />
                &lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />
                &lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />
                &lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />&lt;br />
        &lt;/div>
        
        &lt;iframe src="" name="externo" id="externo" width="1000px">&lt;/iframe>
&lt;/body>
&lt;/html>
</pre>

=) é isso ai.