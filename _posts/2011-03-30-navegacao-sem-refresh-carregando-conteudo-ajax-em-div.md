---
id: 416
title: 'Navegação sem refresh &#8211; carregando conteúdo com ajax em div'
date: 2011-03-30T06:45:28+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=416
permalink: /ajax/navegacao-sem-refresh-carregando-conteudo-ajax-em-div/
dsq_thread_id:
  - "2100773012"
categories:
  - AJAX
tags:
  - navegação
---
Não gosto de escrever sobre isso, mas me sinto obrigado.

Eu pessoalmente evito ao máximo usar _navegação por ajax_, por uma série de problemas causados por isso.
  
**AJAX** é uma metodologia muito interessante, não é uma outra linguagem nova, é apenas um conceito que usa um objeto da **linguagem javascript**.

<!--more-->


  
Aqui, para facilitar o que quero expôr, já que esse artigo é apenas introdução para o próximo, vou utilizar o Framework jQuery, que também não é uma outra linguagem, é apenas, digamos assim uma &#8216;ferramenta&#8217; escrita sob a **linguagem javascript**.

**index.html**

<pre name="code" class="html">&lt;html>
&lt;head>
	&lt;meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />

	&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js">&lt;/script>
	&lt;script type="text/javascript">
	$(document).ready(function(){
		$("#menu a").click(function( e ){
			e.preventDefault();
			var href = $( this ).attr('href');
			$("#content").load( href +" #content");
		});
	});
	&lt;/script>
&lt;/head>
&lt;body>
	&lt;ul id="menu">
		&lt;li>&lt;a href="index.html">Home&lt;/a>&lt;/li>
		&lt;li>&lt;a href="fotos.html">Fotos&lt;/a>&lt;/li>
		&lt;li>&lt;a href="contato.html">Contato&lt;/a>&lt;/li>
	&lt;/ul>&lt;!-- /menu -->
	&lt;div id="content">
		&lt;h1>Bem Vindo!&lt;/h1>
		&lt;p>Essa eh a home desse nome pseudo-site.&lt;/p>
	&lt;/div>&lt;!-- /content -->
&lt;/body>
&lt;/html>
</pre>

Nossa index, contém todo o código jQuery que vamos precisar para carregar o conteúdo na nossa div#content.
  
Para usar a lib jQuery, preciso obrigatoriamente linkar no meu documento a declaração e definição dela, por isso a linha:

<pre name="code" class="javascript:firstLine[5]">&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js">&lt;/script></pre>

Logo depois, aguardo o DOM carregar, pois preciso que os meus elementos existam, para conseguir atrelar eventos e rotinas neles.

<pre name="code" class="javascript:firstLine[7]">$(document).ready(function(){</pre>

E então, uso o seletor jQuery, para me retornar um array de objetos, dos links do meu menu, e aplico uma função no evento onclick de cada um deles: 

<pre name="code" class="javascript:firstLine[8]">$("#menu a").click(function( e ){</pre>

Uma das belezas do jQuery é essa: esconder por trás dos panos os loops. Existem vários elementos ai, porém não estamos vendo como a lib atrela a função elemento a elemento, daí temos essa mágica.

Notem que eu invoco um argumento ali **e**, os métodos jQuery, já retornam o objeto global **window.event** de forma crossbrowser. Com esse objeto, podemos descobrir coisas interessantes da função que disparamos. Algumas propriedades, .keyCode, .target..

<pre name="code" class="javascript:firstLine[9]">e.preventDefault();</pre>

Uso o método **.preventDefault()**, para impedir o comportamento default da tag <a>, que é enviar a requisição pro navegador, este enviar para o servidor, e então acontece o refresh&#8230;

<pre name="code" class="javascript:firstLine[10]">var href = $( this ).attr('href');</pre>

Guardo em uma variavel de escopo local (cada objeto <a>, possui um href para ele), o valor do atributo .href da tag <a>

<pre name="code" class="javascript:firstLine[11]">$("#content").load( href +" #content");</pre>

Agora sim, finalmente faço o ajax.
  
Usei o método .load(), para aproveitar a simplificidade dele. Veja que logo depois do arquivo (href), indico um ID para esse método.

Com isso, consigo ter páginas internas assim:
  
**contato.html**

<pre name="code" class="html">&lt;html>
&lt;head>
	&lt;meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />

&lt;/head>
&lt;body>
	&lt;ul id="menu">
		&lt;li>&lt;a href="index.html">Home&lt;/a>&lt;/li>
		&lt;li>&lt;a href="fotos.html">Fotos&lt;/a>&lt;/li>
		&lt;li>&lt;a href="contato.html">Contato&lt;/a>&lt;/li>
	&lt;/ul><!-- /menu -->
	&lt;div id="content">
		&lt;h1>Contato&lt;/h1>
		&lt;form action="" method="post">
			&lt;label>Nome: &lt;input type="text" name="nome" />&lt;/label>
			&lt;label>E-mail: &lt;input type="text" name="email" />&lt;/label>

			&lt;label>&lt;input type="submit" name="ok" value="OK" />&lt;/label>
		&lt;/form>
	&lt;/div>&lt;!-- /content -->
&lt;/body>
&lt;/html>
</pre>

Graças ao segundo parâmetro do .load(), o jQuery vai fazer um parser do .responseText, e vai jogar dentro do div#content da index.html, apenas o conteudo da div#content do contato.html.

**fotos.html**

<pre name="code" class="html">&lt;html>
&lt;head>
	&lt;meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />

&lt;/head>
&lt;body>
	&lt;ul id="menu">
		&lt;li>&lt;a href="index.html">Home&lt;/a>&lt;/li>
		&lt;li>&lt;a href="fotos.html">Fotos&lt;/a>&lt;/li>
		&lt;li>&lt;a href="contato.html">Contato&lt;/a>&lt;/li>
	&lt;/ul><!-- /menu -->
	&lt;div id="content">
		&lt;h1>Fotos&lt;/h1>


		&lt;a href="index.html">Voltar&lt;/a>
	&lt;/div>&lt;!-- /content -->
&lt;/body>
&lt;/html>
</pre>

Dessa forma, se desativar o suporte a javascript do navegador, o site funciona. O menu te leva para a respectiva página com refresh e tudo mais. Pois não fiz baseado em javascript. Adicionei o javascript por cima de algo que já funcionava. Essa é a maneira correta de desenvolver.

## Caso você esteja tendo problemas com plugins js nas páginas internas

Devido ao grande número de comentários, e pessoas relatando problemas com códigos javascript, que não funcionam, depois que a página interna foi carregada com ajax, usando o código acima. Eu fiz o seguinte post:

[Usando lightbox em página carregada com ajax](http://wbruno.com.br/2011/08/22/usando-lightbox-em-pagina-carregada-ajax/).

Fiz com lightbox no exemplo, porém a dica se aplica a qualquer plugin que vc precisar.
  
Leia, entenda e resolva seu problema.