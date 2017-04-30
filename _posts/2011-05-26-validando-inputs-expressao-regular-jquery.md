---
id: 1034
title: Validando inputs com Expressão Regular com jQuery
date: 2011-05-26T17:19:41+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=1034
permalink: /expressao-regular/validando-inputs-expressao-regular-jquery/
dsq_thread_id:
  - "2100795699"
categories:
  - Expressão Regular
tags:
  - validador
---
Talvez me odeiem por isso, talvez me crucifiquem.. sei lá..
  
Acabei de ver <a href="http://www.jquerymagazine.com.br/artigo.php?id=239" target="_blank">este artigo</a>, pelo Twitter.

Okay, a idéia é bacana, porém existem _falhas_ nesse código apresentado.
  
<!--more-->


  
**Expressões Regulares** são bem úteis, e o método **.replace()** da linguagem javascript, é muito simples de usar.

Vamos&#8230; melhorar a proposta.
  
Afinal de contas, toda vez que critico algo, aparece alguém dizendo &#8216;então faça você&#8217;, lá vai:
  
Não sei se era a intenção do criador, porém o script aceita **espaço**, apesar dele não ter citado isso no comentário.

<pre name="code" class="js">// Somente letras maiúsculas e minúsculas e numeros
	$("#campo4").keyup(function() {
		var valor = $("#campo4").val().replace(/[^a-zA-Z 0-9]+/g,'');
		$("#campo4").val(valor);
	});
</pre>

Nesse outro, aceita **vírgulas**&#8230; achei estranho..

<pre name="code" class="js">// Somente valores definidos
	$("#campo5").keyup(function() {
		var valor = $("#campo5").val().replace(/[^2,4,6,8]+/g,'');
		$("#campo5").val(valor);
	});
</pre>

alguém fora eu, percebeu uma repetição de código ?

<pre name="code" class="js">// Descrição
	$( blablabla ).keyup(function() {
		var valor = $( blablabla ).val().replace(ER,'');
		$( blablabla ).val(valor);
	});
</pre>

certo ?
  
Primeiro passo para melhorar, tornando reaproveitável, é encapsular numa function, e usar a palavra chave **this**, afinal ir no DOM, selecionar 3 vezes o mesmo elemento, é lento.. já que o js nos oferece um ponteiro de graça e muito bom para isso.

Primeiro, corrigindo o problema de performance, e a expressão regular:

<pre name="code" class="js">// Somente valores definidos
	$("#campo5").keyup(function() {
		var $this = $( this ); //armazeno o ponteiro em uma variavel
		var valor = $this.val().replace(/[^2468]+/g,'');
		$this.val( valor );
	});
</pre>

veja que uso uma variavel criada por mim **var $this**, para representar <u>o objeto atual</u>, e assim não precisar ficar indo no dom e procurando, e nem &#8216;rechamando&#8217; o seletor jQuery.

Isso aqui:

<pre name="code" class="js">// Somente letras maiúsculas e minúsculas e numeros</pre>

conseguimos mais facilmente com o modificador **\i**

<pre name="code" class="js">/[^a-z0-9]+/gi</pre>

Okay, hora de dar &#8216;o meu toque&#8217;, no script:

<pre name="code" class="js">&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.6.1/jquery.min.js">&lt;/script>
&lt;script type="text/javascript">
//inspirada na http://php.net/preg_replace
function er_replace( pattern, replacement, subject ){
	return subject.replace( pattern, replacement );
}
$(document).ready(function(){
	$("#campo1").keyup(function() {
		var $this = $( this );
		$this.val( er_replace( /[^0-9]+/g,'', $this.val() ) );
	});
	$("#campo2").keyup(function(){
		var $this = $( this );
		$this.val( er_replace( /[^a-z]+/g,'', $this.val() ) );
	});
	$("#campo3").keyup(function(){
		var $this = $( this );
		$this.val( er_replace( /[^a-z]+/gi,'', $this.val() ) );
	});
	$("#campo4").keyup(function(){
		var $this = $( this );
		$this.val( er_replace( /[^a-z0-9]+/gi,'', $this.val() ) );
	});
	$("#campo5").keyup(function() {
		var $this = $( this );
		$this.val( er_replace( /[^2468]+/g,'', $this.val() ) );
	});
});
&lt;/script>
&lt;style type="text/css">
label { display: block; }
&lt;/style>

	&lt;form action="" method="post">
		&lt;label>&lt;input type="text" value="" id="campo1" />
		somente números&lt;/label>

		&lt;label>&lt;input type="text" value="" id="campo2" />
		somente letras minúsculas&lt;/label>

		&lt;label>&lt;input type="text" value="" id="campo3" />
		somente letras maiúsculas e minúsculas&lt;/label>

		&lt;label>&lt;input type="text" value="" id="campo4" />
		somente letras maiúsculas e minúsculas e numeros&lt;/label>

		&lt;label>&lt;input type="text" value="" id="campo5" />
		somente valores definidos (2,4,6,8)&lt;/label>
	&lt;/form>
</pre>

hum&#8230; ainda estou incomodado.. que tal:

<pre name="code" class="js">jQuery.fn.removeNot = function( settings ){
	var $this = jQuery( this );
	var defaults = {
		pattern: /[^0-9]/,
		replacement: ''
	}
	settings = jQuery.extend(defaults, settings);

	$this.keyup(function(){
		var new_value = $this.val().replace( settings.pattern, settings.replacement );
		$this.val( new_value );
	});
	return $this;
}
$(document).ready(function(){
	$("#campo1").removeNot({ pattern: /[^0-9]+/g });
	$("#campo2").removeNot({ pattern: /[^a-z]+/g });
	$("#campo3").removeNot({ pattern: /[^a-z]+/gi });
	$("#campo4").removeNot({ pattern: /[^a-z0-9]+/gi });
	$("#campo5").removeNot({ pattern: /[^2468]+/g });
});
</pre>

Plugins são fantásticos ne?! lol