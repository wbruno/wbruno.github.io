---
id: 1095
title: 'Afinal, o que é o this ? &#8211; javascript'
date: 2011-06-21T07:00:56+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1095
permalink: /jquery/afinal-e-javascript/
dsq_thread_id:
  - "2100860990"
categories:
  - jQuery
---
Apenas para deixar claro de uma vez por todas.

E tentar diminuir a quantidade de scripts parecidos com isso aqui:

<!--more-->

``` html
<script type="text/javascript"> type="text/javascript" src="jquery-1.4.2.min.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  $('.paragrafo span').hide();
  $('.botao').click(function(){
    $('.botao').val('carregando..');
    window.setTimeout(function(){
      $('.botao').fadeOut();

      $('.paragrafo span').show();
    }, 1000 );
  });
});
</script>

<p class="paragrafo">
  <input type="button" name="botao" value="Click Me" class="botao" />
  <span>Lero Lero</span>
</p>
```

Bem simples:

> No evento onclick do elemento com a class=&#8221;botao&#8221;, disparo uma function, que vai trocar o atributo .value dos elementos com a class botão, pela string: &#8216;carregando&#8217;, e depois de 1 segundo(por causa do atrazo do setTimeout(), esses elementos sumirão da tela, com um efeito de fadeOut();

Encontrei ótimos textos sobre o this:

<a href="http://www.fredericoemidio.com/post/entendendo-javascript-this.aspx" target="_blank">http://www.fredericoemidio.com/post/entendendo-javascript-this.aspx</a>

Porém, o meu intuito é escrever algo mais básico, bem mais nível iniciante mesmo.

Já que um texto escrito neste nível: <a href="http://imasters.com.br/artigo/20785/javascript/compreendendo-a-palavra-chave-this-do-javascript" target="_blank">http://imasters.com.br/artigo/20785/javascript/compreendendo-a-palavra-chave-this-do-javascript</a> não elucida muita coisa, se vc já não tiver um nível considerável de conhecimento.

Bom, voltando.

O script apresentado resolve a questão. Faz oque foi escrito para fazer, mas, e se tivéssemos mais botões?

``` js
<p class="paragrafo">
  <input type="button" name="botao" value="Click Me" class="botao" />
  <span>Lero Lero</span>
</p>
<p class="paragrafo">
  <input type="button" name="botao" value="Click Me" class="botao" />
  <span>Lero Lero</span>
</p>
<p class="paragrafo">
  <input type="button" name="botao" value="Click Me" class="botao" />
  <span>Lero Lero</span>
</p>
```
Então, a ação em 1 deles, dispararia o efeito em todos os outros.

Não é oque queremos. E precisamos entender o motivo disso acontecer.

No caso, o seletor jQuery: **$(&#8216;.botao&#8217;)**, nos retorna um array de objetos que possuem a class=&#8221;botao&#8221;.

E como estamos trabalhando diretamente e sempre com esse array, cada trecho do script, está sendo aplicado a todos os elementos do conjunto, e não apenas ao clicado, como queríamos.

Lhes apresento(ou não), o objeto **this**. Olhe para essa palavra chave como um &#8216;apontador&#8217;, um &#8216;ponteiro&#8217;, que representa <u>o objeto atual</u>, ou seja, **o elemento** com o qual estamos trabalhando nesse exato momento.

``` js
$( this ).val('carregando..');
```

Maravilha! Agora, o nosso carregando.. só será exibido no botão em que clicarmos.

Continuando..

``` js
var $this = $( this );
    $this.val('carregando..');
    window.setTimeout(function(){
      $this.fadeOut();
```

Okay, agora só some o botão que clicamos.. porém e o span ?

continua aparecendo todos os 3, mesmo que só cliquemos em 1 botão.

Nesse caso, vamos usar o nosso ponteiro **this**, para apartir dele, buscarmos o nosso texto:

``` js
$this.next('span').show();
```

E então, uma outra forma, navegando pelo nosso DOM:

``` js
$this.parent('p').find('span').show();
```

Isso é oque todo programador javascript precisa saber de início sobre o this.
