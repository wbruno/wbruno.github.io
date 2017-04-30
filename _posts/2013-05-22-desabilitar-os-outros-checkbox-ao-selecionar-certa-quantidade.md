---
id: 2990
title: Desabilitar os outros checkboxes ao selecionar certa quantidade
date: 2013-05-22T16:45:28+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2990
permalink: /javascript-puro/desabilitar-os-outros-checkbox-ao-selecionar-certa-quantidade/
dsq_thread_id:
  - "2102134845"
categories:
  - Javascript
tags:
  - formulário
---
**Problema:** Desabilitar os outros checkboxes ao selecionar uma certa quantidade deles.

[<img src="/wp-content/uploads/2013/05/a.png" alt="a" width="88" height="109" class="aligncenter size-full wp-image-2992" />](/wp-content/uploads/2013/05/a.png)

Passos:

  1. contar a quantidade de checkboxes selecionados;
  2. verificar no load da página se já tem 2 checks marcados;
  3. somar ou subtrair conforme for clicando nos checkboxes;
  4. se a quantidade de checks marcados for igual a 2, então desabilita todos os outros;
  5. caso contrário(se quantidade de checks selecionados for menor que 2), então os outros devem perder o disabled

Essa é a rotina inclusive para fazer a ida e volta do script. Verificar somando e subtraindo caso o cara tire o checked do checkbox.

<!--more-->

## Solução

<pre class="html">&lt;!doctype html>
&lt;html lang="en">
&lt;head>
	&lt;meta charset="UTF-8">
	&lt;title>&lt;/title>

&lt;style>label { display: block; }&lt;/style>
&lt;script type="text/javascript">
(function(){
	"use strict";

	var marcados = 0;
	var verifyCheckeds = function($checks) {
		if( marcados>=2 ) {
			loop($checks, function($element) {
				$element.disabled = $element.checked ? '' : 'disabled';
			});
		} else {
			loop($checks, function($element) {
				$element.disabled = '';
			});
		}
	};
	var loop = function($elements, cb) {
		var max = $elements.length;
		while(max--) {
			cb($elements[max]);
		}
	}
	var count = function($element) {
		return $element.checked ? marcados + 1 : marcados - 1;
	}
	window.onload = function(){
		var $checks = document.querySelectorAll('input[type="checkbox"]');
		loop($checks, function($element) {
			$element.onclick = function(){
				marcados = count(this);
				verifyCheckeds($checks);
			}
			if($element.checked) marcados = marcados + 1;
		});
		verifyCheckeds($checks);
	}
}());
&lt;/script>
&lt;/head>
&lt;body>

	&lt;label>&lt;input type="checkbox" value="1" />Item 1&lt;/label>
	&lt;label>&lt;input type="checkbox" value="2" />Item 2&lt;/label>
	&lt;label>&lt;input type="checkbox" value="3" />Item 3&lt;/label>
	&lt;label>&lt;input type="checkbox" value="4" />Item 4&lt;/label>
	&lt;label>&lt;input type="checkbox" value="5" />Item 5&lt;/label>
&lt;/body>
&lt;/html>
</pre>

### A função loop

Essa função é a chave do funcionamento do script. Criei ela para interar sob uma coleção de elementos, e então rodar uma função para cada um desses elementos. Assim não preciso ficar repetindo esse loop por diversos lugares do código.

Ela recebe a coleção de elementos e um callback para executar em cada um desses elementos.

<pre class="javascript">var loop = function($elements, cb) {
		var max = $elements.length;
		while(max--) {
			cb($elements[max]);
		}
	}
</pre>

A interface de uso é esta:

<pre class="javascript">loop($elements, function($element) {
	//funcao executada para cada $element
});
</pre>

### A função verifyCheckeds

Se já tiverem sido marcados 2 ou mais checkboxes, ela desabilita os outros checks.

Se não, habilita todos eles. Isso serve para o caso do cara marcar dois e depois desmarcar um, assim a função tira o disabled de todos e o usuário pode selecionar outro checkbox.

### VanillaJS

Apenas js puro. Bem simples, poucas linhas de código e resolvido. =)
