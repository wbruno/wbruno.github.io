---
id: 251
title: O método .live() do jQuery
date: 2011-03-18T16:54:11+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=251
permalink: /jquery/metodo-live-jquery/
dsq_thread_id:
  - "2100772609"
categories:
  - jQuery
tags:
  - framework
---
Caras, como fico impressionado, ao pesquisar por algum assunto que eu gostaria de postar, e encontro logo na primeira página do google 6 entre 10 resultados, exatamente o mesmo conteúdo.

Se não bastasse essa evidente duplicação, o conteúdo nem possui qualidade, com isso, blogs sérios com algo realmente importante a dizer, parecem não encontrar a sua relevância.

Legal, o método **.live()** do jQuery, veio apartir das versões 1.4, existe um plugin chamado <a href="http://plugins.jquery.com/project/livequery" target="_blank">livequery</a> [que eu pessoalmente, nunca usei], o .live() nativo desde então, nos ajuda a <cite>atrelar eventos aos elementos dinamicamente, mesmo que estes não estejam presentes no DOM, no instante do document.ready</cite>

Na prática, o método **.live()**, atrela as funções aos elementos dinâmicamente, no momento em que você tenta chamar.

O motivo desse método existir, é que se eu criar algum elemento com javascript, ou trazer com ajax, esse elemento que não existia no momento do document.ready, e portanto, não teve o evento atrelado, pode ganhar vida.

Exemplo do &#8216;problema:&#8217;

<!--more-->

<pre name="code" class="html">


<head>
  <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js"></script>
  <script type="text/javascript">
  $(document).ready(function(){
  	var i = $('.box').size();
  	$("input[name='add']").click(function(){
  		i++;
  		$('#campos').append('<div class="box">'+i+'</div>');
  	});
  
  	$('.box').click(function(){
  		oi( $( this ).html() );
  	});
  });
  function oi( nome ){
  	alert( 'Oi, eu sou o .box: '+nome );
  }
  </script>
  <style>
  #campos {
  	width: 400px;
  }
  .box {
  	background: #f0f;
  	height: 70px;
  	width: 70px;
  	float: left;
  	margin: 0 10px 10px 0;
  	text-align: center;
  	line-height: 70px;
  }
  
  </style>
  </head>
  <body>
  
  
  	<input type="button" name="add" value="add" />
  	<div id="campos">
  		<div class="box">1</div>
  		<div class="box">2</div>
  	</div><!-- /campos -->
  
  
  </body>
  </html>
  </pre>
  
  
  <p>
    Clique primeiro na caixinha 1 ou na 2, vc verá que é exibido um alert, com o texto que está dentro da div.
  </p>
  
  
  <p>
    Depois vá clicando em [add], serão criados mais elementos, com a autonumeração.
  </p>
  
  
  <p>
    apesar desses novos elementos, serem idênticos aos outros 2 que já existiam, estes novos, não disparam o alert() se clicados.
  </p>
  
  
  <p>
    veja:
  </p>
  
  
  <pre name="code" class="javascript">
	$('.box').click(function(){
		oi( $( this ).html() );
	});</pre>
  
  
  <p>
    É neste trecho que atrelo uma rotina ao evento onclick de todos os elementos que possuirem a class .box
  </p>
  
  
  <p>
    Porém, convém lembrar que os novos elementos, adicionados qndo cliquei no [add], não existiam no instante do document.ready, e portanto, ainda não tiveram o evento atrelado.
  </p>
  
  
  <p>
    Quando vc faz uma requisição ajax, e joga os elementos no documento, com javascript, ocorre o mesmo desse meu exemplo: &#8220;Os elementos não existiam, e por isso, ainda não tem o evento atrelado a eles.&#8221;
  </p>
  
  
  <p>
    <p>
      Note que se eu tivesse feito:
    </p>
    
    
    <p>
      <pre name="code" class="html">
$('#campos').append( '&lt;div class="box" onclick="oi( this.innerHTML );">'+i+'&lt;/div>' );
</pre>
      
      
      <p>
        este problema não aconteceria. Pois a rotina está explicitamente atrelada ao evento ali.
      </p>
      
      
      <p>
        Porém, como isso é uma má prática de programação javascript [misturar camadas, javascript inline..], vamos ao método jQuery de resolver.
      </p>
      
      
      <p>
        Basta trocar:
      </p>
      
      
      <pre name="code" class="javascript">	$('.box').click(function(){</pre>
      
      
      <p>
        por:
      </p>
      
      
      <pre name="code" class="javascript">	$('.box').live('click', function(){</pre>
      
      
      <p>
        Somente isso. =)<br />
        Qualquer coisa comentem!
      </p>