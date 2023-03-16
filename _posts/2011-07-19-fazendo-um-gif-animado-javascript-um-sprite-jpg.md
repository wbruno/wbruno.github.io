---
id: 1199
title: 'Fazendo um &#8216;gif animado&#8217; com javascript e um sprite .jpg'
date: 2011-07-19T07:00:31+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1199
permalink: /javascript-puro/fazendo-um-gif-animado-javascript-um-sprite-jpg/
dsq_thread_id:
  - "2100857940"
categories:
  - Javascript
---
hehe ^^

**about:mozilla** [digite isso na barra de endereços do teu Firefox]
  
Sei lá, pelo menos eu não sabia disso, até hoje.

Okay, fiquei curioso, pesquisei um pouco, li sobre &#8220;<a href="http://pt.wikipedia.org/wiki/O_Livro_de_Mozilla" target="_blank">O Livro de Mozilla</a>&#8220;, ai no finzinho do artigo da Wikipédia, vi isso aqui:

> **Netscape**
  
> Antes do Netscape 1.1, about:mozilla produzia o texto &#8220;Mozilla rulles!&#8221; (Mozilla governa!).
  
> Digitando about:mozilla em uma versão Unix do Netscape o símbolo altera para uma animação do Mozilla vindo por detrás do ícone &#8220;planeta&#8221; e cuspindo fogo. (Imagens visíveis <a href="http://256.com/gray/docs/netscape/mozilla/images.html" target="_blank">aqui</a>)

Fiquei meio triste de não ter visto a animação do dragão subindo por trás do logo do Nestscape, e cuspindo fogo..
  
<!--more-->


  
Mas ai resolvi brincar, e fazer um &#8216;gif animado&#8217;, só que sem o .gif.
  
Okay, preciso começar:

``` html
<html>
<head>
<script type="text/javascript">

</script>
<style type="text/css">

</style>
</head>
<body>
  <div id="mozilla"></div>
</body>
</html>
```

Bom, eu sabia que precisava de um documento .html, de javascript e algum css.
  
E como vou usar o sprite, preciso fazer o sprite:
  
![](http://wbruno.com.br/scripts/sprite_mozilla.jpg)

Beleza, tive a iniciativa. Comecei a fazer. Sabendo usar sprites, sei que o meu container ali **#mozilla**, deve ter uma altura e largura tal, para mostrar apenas &#8216;um frame&#8217; do sprite.

``` css
#mozilla {
  background: url('sprite_mozilla.jpg') no-repeat;
  height: 64px;
  width: 64px;
}
```

Tranquilo ne?!
  
Agora já vejo o dragãozinho, o primeiro frame do filme.

CSS Sprite, é uma técnica que se baseia fortemente na propriedade **background-position**.
  
Então, sei apartir disso, que preciso de um script js capaz de alterar essa propriedade, a cada x tempo.

Hum..**background-position**, em javascript quer dizer: 

``` js
obj.style.backgroundPosition```

e &#8216;a cada x tempo&#8217;, deve me lembrar ou <a href="http://wbruno.com.br/2011/03/11/principio-de-slideshow-settimeout-recursivo/" target="_blank">setTimeout()</a> [nesse caso recursivo], ou <a href="http://wbruno.com.br/2009/08/26/demonstracao-funcao-setinterval-javascript/" target="_blank">setInterval()</a>;

Blz, escolho o setInterval(); preciso criar uma função que altere o position.

``` js
var anima = function(){
  var left = 64*i+i;
  
  id('mozilla').style.backgroundPosition = '-'+left+' top';
  i++;
}
```

A _&#8216;fórmula&#8217;_ é simples. Deixei 1pixel de espaço entre cada frame do sprite. Então somo a minha variavel $i, para representar esse espaço. 64 é a largura de cada frame. $i é um contador que aumenta de 1 em 1. Multiplico o contador pela largura de cada frame, e faço o backgroundPosition se mexer de frame em frame.

### <a href="http://wbruno.com.br/scripts/mozilla1.html" target="_blank">Prévia Online</a>

Tranquilo, ne?!
  
(note que o número embaixo da animação, representa o valor da variavel left, e veja como ele vai arbitrariamente crescendo, até passar os 715px de largura do sprite, para o além e adiante.)

Dai então, só vejo tela em branco. Pois lembrem-se do meu &#8216;no-repeat&#8217; no css.

Se eu tivesse deixado o css assim:

``` css
background: url('sprite_mozilla.jpg');
```

Acontece oque vc imaginou (ou pelo menos deveria ter imaginado). A animação se repete do começo.
  
O dragão escondido, vai aparecendo, cospe fogo. [corte] O dragão escondido, vai aparecendo&#8230;

### <a href="http://wbruno.com.br/scripts/mozilla2.html" target="_blank">Prévia Online</a>

Só que essa animação não me agradou muito, e eu queria que o dragão fosse &#8216;sumindo&#8217; para fazer a volta. E foi isso que fiz:

## <a href="http://wbruno.com.br/scripts/mozilla.html" target="_blank">Demonstração Online</a>

Bom, é isso. Uso conceitual de **css sprite** e da função **setInterval()**.
  
=)