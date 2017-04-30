---
id: 3114
title: Adicionar/Remover campos com javascript
date: 2013-10-29T15:36:49+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3114
permalink: /javascript-puro/adicionarremover-campos-com-javascript/
dsq_thread_id:
  - "2103125749"
categories:
  - Javascript
tags:
  - formulário
---
Rotina bem conhecida e muito usada. Mas implementei de uma forma que ao remover campos já adicionados, os demais não sejam apagados.

<pre>&lt;!doctype html>
&lt;html lang="en">
&lt;head>
	&lt;meta charset="UTF-8">
	&lt;title>Document&lt;/title>
&lt;style>
label { display: block; }
&lt;/style>
&lt;/head>
&lt;body>

&lt;select name="children-qnt" id="children-qnt">
	&lt;option value="0">0&lt;/option>
	&lt;option value="1">1&lt;/option>
	&lt;option value="2">2&lt;/option>
	&lt;option value="3">3&lt;/option>
	&lt;option value="4">4&lt;/option>
	&lt;option value="5">5&lt;/option>
	&lt;option value="6">6&lt;/option>
&lt;/select>
&lt;fieldset id="children">

&lt;/fieldset>&lt;!-- #children -->

&lt;script type="text/javascript" src="http://code.jquery.com/jquery-1.10.2.min.js">&lt;/script>
&lt;script type="text/javascript">
var $chidrenQnt = jQuery('#children-qnt'),
	$children = jQuery('#children');



var Children = {};
Children.container = $children;
Children.add = function(i) {
	while (i--) {
		Children.container.append('&lt;label>idade: &lt;input type="text" name="" />&lt;/label>');
	}
}
Children.remove = function(i) {
	while (i--) {
		Children.container.find('label:last').remove();
	}
}


$chidrenQnt.on('change', function(){
	var $this = jQuery(this),
		i = $this.val(),
		qnt = $children.find('label').length;


	if (qnt > i) {
		Children.remove(qnt - i);
	}
	if (qnt &lt; i) {
		Children.add(i - qnt);
	}
});


&lt;/script>

&lt;/body>
&lt;/html>
</pre>