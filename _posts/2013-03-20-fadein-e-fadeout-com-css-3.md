---
id: 2927
title: FadeIn e FadeOut com css 3
date: 2013-03-20T10:46:00+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2927
permalink: /css/fadein-e-fadeout-com-css-3/
dsq_thread_id:
  - "2101442867"
categories:
  - CSS
---
Um pouco de mágica hoje. Já estamos mais do que acostumados a usar as funções <var>$el.fadeIn()</var> e <var>$el.fadeOut()</var>, nativas do <a href="http://jquery.com/" target="_blank" rel="external">jQuery</a>, para fazer os efeitos de **fadeIn** e **fadeOut**. Que nada mais é, do que aquela transição suave de uma imagem opaca, para um &#8220;nada&#8221;. 

Em css, isso é representado pela propriedade <var>opacity</var>.

Mas estou aqui hoje para lhes contar que não é mais necessário isso nos dias de hoje.
  
A especificação css3, trouxe uma nova propriedade chamada **transition**. E ela faz milagres, se formos pensar na complexidade e performance do código javascript equivalente que temos que escrever para chegar no mesmo resultado.

É tudo bem simples. Dado uma outra propridade, com valores numéricos, como <var>width, height, opacity, left, top</var>&#8230; o transition faz uma transição suave entre 2 valores. Essa propriedade css aceita um tempo em segundos do quanto &#8220;o efeito&#8221; irá demorar para acabar.

## Exemplo

``` js
<img src="http://www.clipartsegifs.com.br/cliparts/variados/garfield/garfield_02.jpg" id="img-fade" />
<button id="btn-fade">FadeOut</button>

<style>
#img-fade { transition: 2s; }
.fade-out { opacity: 0; }
.fade-in { opacity: 1; }
</style>

<script>
var id = function(el) {
  return document.getElementById( el );
}
var $btn = id('btn-fade'),
  $img = id('img-fade');

$btn.onclick = function(){
  var $this = this;


  if( $img.className ==='fade-out' ){
    $img.className = 'fade-in';
    $this.innerHTML = 'FadeOut';
  } else {
    $img.className = 'fade-out';
    $this.innerHTML = 'FadeIn';
  }
}
</script>
```

É isso, já usou ? comente.