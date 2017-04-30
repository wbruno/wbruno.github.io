---
id: 578
title: Entendendo erros do validador HTML w3c
date: 2011-04-05T07:00:23+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=578
permalink: /html/entendendo-erros-validador-html-w3c/
dsq_thread_id:
  - "2115948060"
categories:
  - HTML
tags:
  - validador
  - w3c
  - xhtml
---
Boas galera!

Existem 3 tipos de **DOCTYPE**: Frameset, Transitional e Strict.

[<img src="/wp-content/uploads/2011/04/xhtml-150x150.png" alt="" title="xhtml" width="150" height="150" class="alignright size-thumbnail wp-image-602" />](/wp-content/uploads/2011/04/xhtml.png)

Vou me focar em **xHTML Strict**, pois é o que eu costumo usar. Nunca passei pelo Transitional, e sempre gostei muito da <a href="http://pt.wikipedia.org/wiki/XHTML" target="_blank">proposta do xHTML</a>. Lembro da época em que discutíamos sobre <a href="http://www.midiadigital.com.br/blog/web-standards/novos-padroes-e-funcionalidades-da-web-xhtml2-versus-html5/" target="_blank">xHTML2 versus HTML5</a>. A rigidez da especificação, te obriga a entender melhor, sutilezas e conceitos que as outras deixam passar.

Acredito que a maioria de vocês, já use um dos 2. Se você usa o Transitional, fica a minha dica de mudar para o Strict, se você já está no Strict, então entenda o motivo dos erros.

<!--more-->



Servir o documento com headers de XML, é bem interessante, já que qualquer erro, gera uma falha de XML, porém não é nada convencional.

[<img src="/wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-11.27.09-AM.png" alt="" title="Screen shot 2011-04-04 at 11.27.09 AM" width="739" height="234" class="aligncenter size-full wp-image-601" srcset="/wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-11.27.09-AM.png 739w, /wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-11.27.09-AM-300x94.png 300w" sizes="(max-width: 739px) 100vw, 739px" />](/wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-11.27.09-AM.png)

O meu crime foi não ter fechado a tag <img />.

<pre name="code" class="html">&lt;img src="images/wbruno-logo.png" alt="" id="logo"></pre>

Antecessora mais próxima do do <u></div><!&#8211; /main &#8211;></u>, daí o erro foi disparado nele. Para mim:

> _Conhecer bem xHTML, te faz ser melhor em HTML_

### HTML4

<pre name="code" class="html">&lt;!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
  "http://www.w3.org/TR/html4/strict.dtd">
</pre>

### xHTML 1.0

<pre name="code" class="html">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
</pre>

### xHTML 1.1

<pre name="code" class="html">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN"
    "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
</pre>

Vou fazer via <a href="http://validator.w3.org/#validate_by_input" target="_blank">Direct Input</a>.

Esta é a <a href="http://validator.w3.org/check?verbose=1&#038;uri=http%3A%2F%2Fwww.wbruno.com.br%2Fscripts%2Fxhtml-minimo.html" target="_blank">marcação mínima de um documento</a>:

<pre name="code" class="html">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
&lt;html xmlns="http://www.w3.org/1999/xhtml">
&lt;head>
	&lt;title>wbruno&lt;/title>
	&lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
&lt;/head>
&lt;body>


&lt;/body>
&lt;/html>
</pre>

a tag <title> e a tag <meta /> de charset, são obrigatórias. Tomemos como base o documento que apresentei.

<pre name="code" class="html:firstLine[9]">&lt;br></pre>

Passando no validador: [<img src="/wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-2.21.36-PM-1024x338.png" alt="" title="Screen shot 2011-04-04 at 2.21.36 PM" width="695" height="229" class="aligncenter size-large wp-image-614" srcset="/wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-2.21.36-PM-1024x338.png 1024w, /wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-2.21.36-PM-300x99.png 300w, /wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-2.21.36-PM.png 1432w" sizes="(max-width: 695px) 100vw, 695px" />](/wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-2.21.36-PM.png)

Para não ficar muito extenso, vou dividir em mais uma parte esse post.

[Continua&#8230;.](http://www.wbruno.com.br/2011/04/07/entendendo-erros-validador-html-w3c-parte-2/)
