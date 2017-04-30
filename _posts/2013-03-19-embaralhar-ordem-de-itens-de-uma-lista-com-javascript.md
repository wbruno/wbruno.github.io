---
id: 2926
title: Embaralhar ordem de itens de uma lista com javascript
date: 2013-03-19T21:18:55+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2926
permalink: /javascript-puro/embaralhar-ordem-de-itens-de-uma-lista-com-javascript/
dsq_thread_id:
  - "2116321692"
categories:
  - Javascript
---
Hoje no iMasters um cara pediu para desordenar itens de uma lista html.
  
Bom, desordenar um array é simples, e array em javascript é um objeto, logo desordenar um objeto é simples também.

Basta pegarmos os itens da lista, desordena-los, remove-los do DOM, e então inseri-los novamente.

## Versão com javascript puro

<pre name="code" class="javascript">&lt;ul id="items">
	&lt;li>1&lt;/li>
	&lt;li>2&lt;/li>
	&lt;li>3&lt;/li>
	&lt;li>4&lt;/li>
	&lt;li>5&lt;/li>
	&lt;li>6&lt;/li>
	&lt;li>7&lt;/li>
	&lt;li>8&lt;/li>
	&lt;li>9&lt;/li>
	&lt;li>10&lt;/li>
&lt;/ul>

&lt;script>
(function(){
	/**
	 * Deixar os itens do array em ordem aleatoria
	 */
	Array.prototype.shuffle = function() {
	  var i = this.length, j, tempi, tempj;
	  if ( i == 0 ) return this;
	  while ( --i ) {
	     j       = Math.floor( Math.random() * ( i + 1 ) );
	     tempi   = this[i];
	     tempj   = this[j];
	     this[i] = tempj;
	     this[j] = tempi;
	  }
	  return this;
	}

	/**
	 * Inicialização das variaveis
	 */
	var items = document.getElementById('items'),
		lis = items.getElementsByTagName('li'),
		arr = [],
		max = lis.length;

	/**
	 * Colocando o html colection em um array
	 */
	for( var i = 0; i&lt;max; i++ ){
		arr[i] = lis[i];
	}
	arr = arr.shuffle();

	/**
	 * Removendo os items
	 */
	while (items.firstChild) {
	    items.removeChild(items.firstChild);
	}

	/**
	 * Inserindo novamente no DOM
	 */
	while( i-- ){
		items.appendChild( arr[i] );
	}

})();
&lt;/script>
</pre>

## Versão com jQuery

<pre name="code" class="javascript">&lt;ul id="items">
	&lt;li>1&lt;/li>
	&lt;li>2&lt;/li>
	&lt;li>3&lt;/li>
	&lt;li>4&lt;/li>
	&lt;li>5&lt;/li>
	&lt;li>6&lt;/li>
	&lt;li>7&lt;/li>
	&lt;li>8&lt;/li>
	&lt;li>9&lt;/li>
	&lt;li>10&lt;/li>
&lt;/ul>

&lt;script src="http://code.jquery.com/jquery-1.8.0.min.js">&lt;/script>
&lt;script>
var shuffle = function( el ) {
 var i = el.length, j, tempi, tempj;
 if ( i == 0 ) return el;
 while ( --i ) {
    j       = Math.floor( Math.random() * ( i + 1 ) );
    tempi   = el[i];
    tempj   = el[j];
    el[i] = tempj;
    el[j] = tempi;
 }
}

var arr = jQuery('#items').find('li');
shuffle( arr );
jQuery('#items').html( arr );
&lt;/script>
</pre>