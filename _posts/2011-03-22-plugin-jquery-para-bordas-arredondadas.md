---
id: 305
title: Plugin jQuery para bordas arredondadas
date: 2011-03-22T10:24:27+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=305
permalink: /jquery/plugin-jquery-para-bordas-arredondadas/
categories:
  - jQuery
tags:
  - plugin
---
Um plugin que criei para fazer o efeito de bordas arredondadas.

Ele é bem simples, apenas adiciona uma DIV com class .top e/ou .bottom, no elemento que vc o chamar.
  
<!--more-->

<pre name="code" class="javascript">jQuery.fn.round = function( settings ){
	var defaults = {
		top: true,
		bottom: true
	}
	settings = jQuery.extend(defaults, settings);
	$this = $( this );

	if( settings.top ) jQuery( $this ).prepend( '&lt;div class="top">&lt;/div>' );
	if( settings.bottom ) jQuery( $this ).append( '&lt;div class="bottom">&lt;/div>' );

	//jQuery( $this ).css({zIndex: 1});
	return $this;

}</pre>

modo de usar:

<pre name="code" class="javascript">$(document).ready(function(){
	$("#top").round({top: false});
	$("#content").round();
});</pre>

a mágica de novo, está toda do lado do **CSS**.
  
ali, como mandei um top: false; para o id=#top, só será criada a div .bottom.

No #content, como não mandei nada, será criada as duas.
  
Toda a estilização para deixar redondo mesmo, deve ser feito no css. Nesse caso, qndo uso esse meu plugin, costumo trabalhar com background.
  
Lembrando de dar um position: relative para o container, posicionando com absolute essas divs extras.

<pre name="code" class="html">.top,
.bottom {
	height: 7px;
	position: absolute;
	left: 0;
	z-index: 2;
	width: 970px;
}
.top {
	background-image: url('../images/bg-box-top.jpg') left top no-repeat;
	top: 0;
}
.bottom {
	background-image: url('../images/bg-box-bottom.jpg') left bottom no-repeat;
	bottom: 0;
}</pre>

A vantagem desse plugin, é que vc manterá a tua marcação limpa, sem essas divs &#8216;vazias&#8217;, e sem semântica.
  
Não fiz nenhum css no plugin, para deixá-lo mais personalizável e robusto, visto que você terá que saber css para usá-lo, portanto, não é bem um plug and play, mas um plug study and play.