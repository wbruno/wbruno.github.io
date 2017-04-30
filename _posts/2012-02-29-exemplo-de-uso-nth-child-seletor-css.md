---
id: 1808
title: Exemplo de uso do nth-child seletor css
date: 2012-02-29T15:19:00+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1808
permalink: /jquery/exemplo-de-uso-nth-child-seletor-css/
dsq_thread_id:
  - "2102324355"
categories:
  - jQuery
---
Selecionar o terceiro elemento de cada lista, para alterar alguma coisa do css dele.

Usar: .eq(3) é o mesmo que :nth-child(3), oq queremos é o **3n**

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js">&lt;/script>
&lt;script type="text/javascript">
jQuery(document).ready(function(){
	jQuery('.lista li:nth-child(3n)').css('background','#f0f');
});
&lt;/script>
&lt;style type="text/css">
.lista { width: 180px; }
.lista li {
	background: #f00;
	margin: 5px;
	width: 50px;
	height: 50px;
	float: left;
}
.clear { clear: both; }
&lt;/style>
&lt;/head>
&lt;body>
	&lt;h2 class="clear">Primeira lista&lt;/h2>
	&lt;ul class="lista">
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
	&lt;/ul>
	&lt;h2 class="clear">Segunda lista&lt;/h2>
	&lt;ul class="lista">
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
	&lt;/ul>
	&lt;h2 class="clear">Terceira lista&lt;/h2>
	&lt;ul class="lista">
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
		&lt;li>&lt;/li>
	&lt;/ul>
&lt;/body>
&lt;/html>
</pre>