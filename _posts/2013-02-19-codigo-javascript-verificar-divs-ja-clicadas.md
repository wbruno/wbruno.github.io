---
id: 2915
title: Código JavaScript verificar divs já clicadas
date: 2013-02-19T14:18:26+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2915
permalink: /javascript-puro/codigo-javascript-verificar-divs-ja-clicadas/
dsq_thread_id:
  - "2100840379"
categories:
  - Javascript
---
Um cara pediu no fórum imasters, era rapidinho, ai fiz um exemplo.

Ao clicar em cada div, ela vai ganhando uma class de &#8220;ativa&#8221;.
  
Ao selecionar todas as 3, aparece uma mensagem abaixo de todas.

É possível fazer a volta, e fazer desselecionar, mas deixo para vcs comentarem aqui, caso alguém peça eu implemento também.

``` html
<style>
  .click-me { 
    width: 100px; height: 100px; 
    margin: 10px; 
    border: 1px solid #000;
    float: left;
  }
  .is-active { border: 1px solid #f00; }
  #result {
    border: 1px solid #000;
    display: none;
    clear: both;
    padding: 40px;
  }
</style>
<script>
(function(){
  var count = 0;

  var clickMe = function(){
    this.className = 'click-me is-active';
    count += 1;
    
    verifyDivs();
  }
  var verifyDivs = function(){
    if( count===3 ){
      document.getElementById('result').style.display = 'block';
    }    
  }
  window.onload = function(){
    var divs = document.getElementsByClassName('click-me');
    for( var i=0; i<divs.length; i++ ){
      divs[i].onclick = clickMe;
    }
  }  
})();
</script>

<div class="click-me"></div>
<div class="click-me"></div>
<div class="click-me"></div>

<div id="result">Resultado</div>
```