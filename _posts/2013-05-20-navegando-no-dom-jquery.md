---
id: 2962
title: 'Navegando no DOM &#8211; jQuery'
date: 2013-05-20T08:00:57+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2962
permalink: /jquery/navegando-no-dom-jquery/
dsq_thread_id:
  - "2101112109"
categories:
  - jQuery
tags:
  - dom
---
Nós já entendemos [o que é o this ? – javascript](http://wbruno.com.br/javascript-puro/afinal-e-javascript/), e agora vou explicar melhor como **navegar no DOM**.

Bom nada melhor do que começar com <a href="http://api.jquery.com/category/traversing/tree-traversal/" rel="nofollow">a documentação oficial</a> sobre os métodos jQuery.

<!--more-->

Vou me focar em apenas alguns mais importantes e mais usados, pois entendendo o conceito fica fácil usar qualquer um deles.

## A árvore DOM

Para entendermos como navegar no DOM, temos que nós lembrar da <a href="http://tableless.com.br/tenha-o-dom/" rel="nofollow">árvore</a>:

[<img src="/wp-content/uploads/2013/05/DOMTree.gif" alt="DOMTree" width="800" height="354" class="aligncenter size-full wp-image-2974" />](/wp-content/uploads/2013/05/DOMTree.gif)

Fazendo uma leitura rápida, da direita para a esquerda:

O elemento <var>em</var>(em roxo), é filho do parágrafo <var>p</var>, que é irmão do <var>h1</var> e do outro <var>p</var>, que são filhos diretos do <var>body</var> que por sua vez é filho do <var>html</var>.

Simples assim. Da esquerda para a direita, vemos que o <var>head</var> e o <var>body</var>, são irmãos entre si e filhos do <var>html</var>. Tranquilo, ne?!

## $(seletor).find()

Esse método procura **elementos filhos** apartir do elemento <var>$(seletor)</var>.

Imagine o seguinte html:

<pre class="html">&lt;p>&lt;span>clique aqui&lt;/span> para ler: &lt;em>em 1&lt;/em>&lt;/p>
&lt;p>&lt;span>clique aqui&lt;/span> para ler: &lt;em>em 2&lt;/em>&lt;/p>
&lt;p>&lt;span>clique aqui&lt;/span> para ler: &lt;em>em 3&lt;/em>&lt;/p>
&lt;p>&lt;span>clique aqui&lt;/span> para ler: &lt;em>em 4&lt;/em>&lt;/p>
</pre>

Quero clicar na palavra &#8220;clique aqui&#8221;, e mostrar em um alert o valor da tag em.

Como o <var>em</var> é **filho** da tag <var>p</var>, posso usar o método <var>.find()</var>, apartir do this(o próprio parágrafo, pois o evento foi disparado nele).

<pre class="html">&lt;!doctype html>
&lt;html lang="en">
&lt;head>
	&lt;meta charset="UTF-8">
	&lt;title>Document&lt;/title>

	&lt;script src="http://code.jquery.com/jquery-1.9.1.min.js">&lt;/script>

&lt;script type="text/javascript">
jQuery(document).ready(function(){
	jQuery('p').on('click', function(){
		var $this = $(this);//o proprio parágrafo

		alert( $this.find('em').text() );
	});
});
&lt;/script>
&lt;style type="text/css">
span { text-decoration: underline; color: #05f; cursor: pointer; }
em { border: 1px solid #000; padding: 0 5px; }
&lt;/style>
&lt;/head>
&lt;body>
	&lt;p>&lt;span>clique aqui&lt;/span> para ler: &lt;em>em 1&lt;/em>&lt;/p>
	&lt;p>&lt;span>clique aqui&lt;/span> para ler: &lt;em>em 2&lt;/em>&lt;/p>
	&lt;p>&lt;span>clique aqui&lt;/span> para ler: &lt;em>em 3&lt;/em>&lt;/p>
	&lt;p>&lt;span>clique aqui&lt;/span> para ler: &lt;em>em 4&lt;/em>&lt;/p>
&lt;/body>
&lt;/html>
</pre>

Irá aparecer na tela um alert com o texto de cada em. Note o código:

<pre class="javascript">$this.find('em').text()</pre>

Da direita para a esquerda novamente:

<var>.text()</var> retorna o texto dentro uma tag html.

<var>(&#8216;em&#8217;)</var> é a tag <em> em si.

<var>.find</var> é a função que estamos falando nesse tópico. Ela procura **filhos**.

<var>$this</var> é o elemento parágrafo, pois o click foi disparado nele: <var>jQuery(&#8216;p&#8217;).on(&#8216;click&#8217;, function(){</var>

## $(seletor).next()

Esse método pega o **próximo** elemento na árvore do DOM. Ou seja o irmão da direita, levando em consideração a ordem em que escrevemos o nosso html.

<pre class="html">&lt;p>&lt;span>clique aqui&lt;/span> para ler: &lt;em>em 1&lt;/em>&lt;/p></pre>

Nesse html acima, o <var>span</var> é irmão do <var>em</var>. Então apartir do span, o em é o _next_ dele.

<pre class="javascript">jQuery('span').on('click', function(){
	var $this = $(this);

	alert( $this.next('em').text() );
});
</pre>

Aqui como o click foi disparado no span, o this é o próprio span, e o next apartir do span é o em.

## $(seletor).parent()

Bem simples até aqui. Nos códigos acima eu busquei o elemento em diretamente apartir da tag alvo do evento click. Mas em situações um pouco mais complicadas, não dá para usar o find() e nem o next() tão diretamente assim.

A solução é **voltar para o pai**, e apartir dele achar o que está precisando.

<pre class="javascript">jQuery('span').on('click', function(){
	var $this = $(this);

	alert( $this.parent('p').find('em').text() );
});
</pre>

Continuo disparando o click no span, então o this é o span.

Mas primeiro eu volto para o parágrafo pai do span, e apartir do parágrafo eu procuro o em que é filho dele.

Note que as 3 versões do código produzem a mesma saida. Ao clicar em &#8220;clique aqui&#8221;, aparece no alert o texto do elemento em.

## $(seletor).parents()

O método <var>.parents()</var> volta **mais de um pai**, ou seja, sobe vários níveis na árvore DOM.

O html do meu exemplo era bem simples, sendo o span filho direto do parágrafo, então só o .parent() já resolvia. Mas se eu tivesse que subir vários níveis, procurando tags avós, bisavós então é o método .parents() que resolve a questão.

Vale lembrar que o .find() acha filhos, netos, bisnetos sem problema. Então para entrar varios niveis filhos, o .find() serve também.

## $(seletor).siblings()

O método .siblings() retorna os elementos **irmãos** do elemento $(seletor).

<pre name="html">&lt;!doctype html>
&lt;html lang="en">
&lt;head>
	&lt;meta charset="UTF-8">
	&lt;title>Document&lt;/title>

	&lt;script src="http://code.jquery.com/jquery-1.9.1.min.js">&lt;/script>

&lt;script type="text/javascript">
jQuery(document).ready(function(){
	jQuery('p').on('click', function(){
		var $this = $(this);

		$this.addClass('red');
		$this.siblings('p').removeClass('red');
	});
});
&lt;/script>
&lt;style type="text/css">
.red { color: #f00; }
&lt;/style>
&lt;/head>
&lt;body>
	&lt;p>lorem ipsum - clique aqui&lt;/p>
	&lt;p>lorem ipsum - clique aqui&lt;/p>
	&lt;p>lorem ipsum - clique aqui&lt;/p>
	&lt;p>lorem ipsum - clique aqui&lt;/p>
&lt;/body>
&lt;/html></pre>

Note que eu adiciono a classe red no elemento clicado:

<pre class="javascript">$this.addClass('red');</pre>

e removo a classe red de todos os irmãos dele:

<pre class="javascript">$this.siblings('p').removeClass('red');</pre>

Assim apenas o clicado fica com a cor vermelha.

## Conclusão

Você pode combinar .parent() com .siblings(), para pegar os irmãos do pai do elemento em que vc estava, pode usar .parents() para voltar mais de um nível, usar .find() para entrar quantos níveis de filhos precisar, e então interagir melhor com o seu DOM.
