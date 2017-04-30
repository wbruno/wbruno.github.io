---
id: 968
title: 'Input de destinatários[para] do hotmail'
date: 2011-05-19T07:00:10+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=968
permalink: /css/input-de-destinatariospara-hotmail/
categories:
  - CSS
---
Sempre achei &#8216;bonito&#8217;, o input onde adicionamos os destinatários no hotmail.

Um dia, estava &#8216;sem fazer muita coisa&#8217;, e resolvi reproduzir o efeito daquele input.
  
[<img src="http://wbruno.com.br/wp-content/uploads/2011/05/input.jpg" alt="" title="input" width="767" height="135" class="aligncenter size-full wp-image-969" srcset="http://wbruno.com.br/wp-content/uploads/2011/05/input.jpg 767w, http://wbruno.com.br/wp-content/uploads/2011/05/input-300x52.jpg 300w" sizes="(max-width: 767px) 100vw, 767px" />](http://wbruno.com.br/wp-content/uploads/2011/05/input.jpg)
  
<!--more-->

**index.html**

<pre name="code" class="html">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
	"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
&lt;html xmlns="http://www.w3.org/1999/xhtml">
&lt;head>
	&lt;title>Input Hotmail&lt;/title>
	&lt;link type="text/css" href="main.css" rel="stylesheet" />
	&lt;!--[if IE 6]>
	&lt;style type="text/css">
	#emails #cntmail { top: 3px; left: 74px; }
	&lt;/style>
	&lt;![endif]-->
&lt;/head>
&lt;body>
	&lt;form action="" method="post">
		&lt;fieldset>
			&lt;label id="meu">meu_email@hotmail.com &lt;img src="seta.gif" alt="" />&lt;/label>
			&lt;label id="emails">&lt;span>Para: &lt;/span>
				&lt;input type="text" name="email" />
					&lt;span id="cntmail">
						&lt;span>email@provedor.com
							&lt;img src="edit.gif" alt="" class="edit" />
							&lt;img src="del.gif" alt="" class="del" />
						&lt;/span>
					&lt;/span>
			&lt;/label>&lt;!-- /emails -->
			&lt;label>&lt;span>Assunto: &lt;/span>
				&lt;input type="text" name="assunto" />&lt;/label>
		&lt;/fieldset>
	&lt;/form>


&lt;/body>
&lt;/html>
</pre>

**main.css**

<pre name="code" class="css">* {
	margin: 0;
	padding: 0;
	list-style: none;
	border: none;
}
body {
	font: 13px Tahoma, Arial, sans-serif;
	margin: 50px;
}
fieldset {
	border: 1px solid #cbcbcb;
	padding: 10px 15px;
}
label {
	display: block;
	padding-left: 20px;
	margin: 1px;
}
label span {
	width: 50px;
	display: inline-block;
	text-align: right;
}
input {
	background: #fff;
	font: 13px Tahoma, Arial, sans-serif;
	border: 1px solid #cbcbcb;
	width: 600px;
	padding: 2px 5px;
	color: #2a2a2a;
	height: 20px;
	margin-left: 2px;
}
#meu {
	color: #2a2a2a;
	font-size: 19px;
	padding: 0 0 5px 0;
}
#emails {
	position: relative;
	height: 30px;
}
#emails input {
	padding-left: 165px;
	width: 440px;
}
#emails #cntmail {
	position: absolute;
	top: 2px;
	left: 78px;
	width: auto;
}
#cntmail span {
	border: 1px solid #bbd8fb;
	background: #f3f7fd;
	color: #2a2a2a;
	padding: 2px 5px;
	width: auto;
}
#cntmail img {
	cursor: pointer;
}
</pre>

Cada destinatário, é um <span> dentro do **span#cntmail**. Cada vez que adicionarmos um email &#8216;no input&#8217;, precisamos aumentar o padding-left dele, para que a digitação do próximo email comece após os emails já adicionados.

## <a href="http://www.wbruno.com.br/scripts/msn/" target="_blank">Demonstração Online</a>