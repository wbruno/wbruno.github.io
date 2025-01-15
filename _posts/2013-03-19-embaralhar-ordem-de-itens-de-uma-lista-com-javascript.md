---
id: 2926
title: Embaralhar ordem de itens de uma lista com javascript
date: 2013-03-19T21:18:55+00:00
author: wbruno
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

``` js
<ul id="items">
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
  <li>6</li>
  <li>7</li>
  <li>8</li>
  <li>9</li>
  <li>10</li>
</ul>

<script>
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
  for( var i = 0; i<max; i++ ){
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
</script>
```

## Versão com jQuery

``` js
<ul id="items">
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
  <li>6</li>
  <li>7</li>
  <li>8</li>
  <li>9</li>
  <li>10</li>
</ul>

<script src="http://code.jquery.com/jquery-1.8.0.min.js"></script>
<script>
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
</script>
```
