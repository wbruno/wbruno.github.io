---
id: 1803
title: 'Controlando show/hide com css &#8211; Deixando para o javascript apenas a troca de uma classe pai'
date: 2012-02-28T14:43:16+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1803
permalink: /javascript-puro/controlando-showhide-css-deixando-para-javascript-apenas-troca-de-uma-classe-pai/
dsq_thread_id:
  - "2101063004"
categories:
  - Javascript
---
Boas =)

A minha proposta aqui, é controlar toda a lógica do show/hide com css.
  
Em vez de fazermos malabarismos com coisas como:
  
<!--more-->

<pre name="code" class="javascript">document.getElementById("Carro").className = "invisivel";
        document.getElementById("Moto").className = "invisivel";
        document.getElementById("Pesados").className = "invisivel";
        document.getElementById("Agrícolas").className = "invisivel";
        document.getElementById("selecione").className = "invisivel";
        document.getElementById(div).className = "visivel";
</pre>

E ai, qndo tiver q mostrar mais de um elemento a cada option do select, recorrer a colocar mais linhas/parâmetros no js.
  
O javascript que proponho é o seguinte:

<pre name="code" class="javascript">function id( obj ){ return document.getElementById( obj ); }
window.onload = function(){
	id('escolha').onchange = function(){
		id('pai').className = this.value;
	}
}</pre>

E conforme queiramos mais elementos a serem mostrados, ou mais regras, não temos que alterar absolutamente nada no js.
  
Apenas no html, e no css.
  
Veja que toda a lógica de mostrar/esconder, está no css:

<pre name="code" class="css">p, #lista li { display: none; }

.carros #palio, 
.carros #punto,
.carros #gol,
.carros #volks { display: block; }

.animais #gato, 
.animais #cao,
.animais #vet { display: block; }
/* deixei separado apenas para facilitar o entendimento */
.linguagens #ajax, 
.linguagens #js,
.linguagens #css,
.linguagens #programador { display: block; }</pre>

A primeira regra css, esconde tudo.
  
As demais, vão dando block, conforme uma classe pai. Exatamente a que estamos alterando via js.

É isso. O que vc acha dessa abordagem ?

<pre name="code" class="html">&lt;html>
&lt;head>
	&lt;title>Show/Hide com css&lt;/title>
&lt;script type="text/javascript">
function id( obj ){ return document.getElementById( obj ); }
window.onload = function(){
	id('escolha').onchange = function(){
		id('pai').className = this.value;
	}
}
&lt;/script>
&lt;style type="text/css">
p, #lista li { display: none; }


.carros #palio, 
.carros #punto,
.carros #gol,
.carros #volks { display: block; }

.animais #gato, 
.animais #cao,
.animais #vet { display: block; }

.linguagens #ajax, 
.linguagens #js,
.linguagens #css,
.linguagens #programador { display: block; }

&lt;/style>
&lt;/head>
&lt;body>
	&lt;select name="escolha" id="escolha">
		&lt;option value="">Esconder todos&lt;/option>
		&lt;option value="carros">Carros&lt;/option>
		&lt;option value="animais">Animais&lt;/option>
		&lt;option value="linguagens">Linguagens&lt;/option>
	&lt;/select>
	
	&lt;div id="pai">
		&lt;ul id="lista">
			&lt;li id="palio">Palio&lt;/li>
			&lt;li id="punto">Punto&lt;/li>
			&lt;li id="gol">Gol&lt;/li>
			
			&lt;li id="gato">Gato&lt;/li>
			&lt;li id="cao">Cão&lt;/li>
			
			&lt;li id="ajax">AJAX&lt;/li>
			&lt;li id="js">JS&lt;/li>
			&lt;li id="css">CSS&lt;/li>
		&lt;/ul>&lt;!-- /lista -->
		
		&lt;p id="volks">Volks&lt;/p>
		
		&lt;p id="vet">Veterinária&lt;/p>
		
		&lt;p id="programador">Programador&lt;/p>
	&lt;/div>
&lt;/body>
&lt;/html></pre>

## <a href="http://wbruno.com.br/scripts/showhidecss.html" target="_blank">Demonstração</a>