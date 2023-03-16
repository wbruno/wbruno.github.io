---
id: 374
title: Adicionar legendas de imagens, atributo alt com javascript
date: 2011-03-27T14:57:19+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=374
permalink: /javascript-puro/adicionar-legendas-de-imagens-atributo-alt-javascript/
dsq_thread_id:
  - "2102667884"
categories:
  - Javascript
---
Comentem galera!

Vi que a série de posts &#8220;Criando um plugin jQuery&#8221; <a href="http://plugins.jquery.com/project/simpleplaceholder" target="_blank">SimplePlaceHolder</a>, foi bem aceita. Gostaria de opiniões, sobre o que devo escrever, ou onde é a dificuldade de vcs.

Vamos lá.

**Problema:**

_</p>

> Possuo um conjunto de miniatura de imagens no HTML.

> Gostaria de uma rotina que adicionasse automaticamente uma legenda, para cada uma dessas imagens, baseada no atributo alt da tag img.

</em>

<!--more-->



Por partes novamente:

_</p>

> Possuo um conjunto de miniatura de imagens no HTML.

</em>

``` html
<html>
<head>
  <style type="text/css">
  * { margin: 0; padding: 0; list-style: none; }
  body { font: 12px Arial, Verdana, sans-serif; }
  #fotos {
    width: 630px;
    margin: 0 auto;
  }
  #fotos li {
    float: left;
    margin: 0 10px 10px 0;
    background: #efefef;
    padding-bottom: 25px;
    position: relative;
  }
  #fotos a {
    width: 200px;
    height: 150px;
    overflow: hidden;
    display: block;
  }
  #fotos img {
    border: none;
  }
  #fotos p {
    position: absolute;
    bottom: 5px;
    left: 10px;
  }
  </style>
  <script type="text/javascript">

  </script>
</head>
<body>
  <ul id="fotos">
    <li><a href="images/01.jpg"><img src="images/thumbs/01.jpg" alt="Céu" /></a><p></p></li>
    <li><a href="images/02.jpg"><img src="images/thumbs/02.jpg" alt="Queda de agua" /></a><p></p></li>
    <li><a href="images/03.jpg"><img src="images/thumbs/03.jpg" alt="Universo" /></a><p></p></li>
    <li><a href="images/04.jpg"><img src="images/thumbs/04.jpg" alt="Praia" /></a><p></p></li>
    <li><a href="images/05.jpg"><img src="images/thumbs/05.jpg" alt="Montanhas" /></a><p></p></li>
    <li><a href="images/06.jpg"><img src="images/thumbs/06.jpg" alt="Verde, agua" /></a><p></p></li>
  </ul><!-- /foto -->
</body>
</html>
```

Legal, o html está ali.

Todo preparado, só precisamos fazer a nossa rotina javascript que vai:

_</p>

> adicionasse automaticamente uma legenda

</em>

Como sempre, para mantermos o nosso script de acordo com as boas normas de desenvolvimento javascript, não vamos misturar javascript com o html. Vai ficar tudo na seção HEAD do documento, e sem declarar eventos inline.

Sabemos que o documento é carregado de cima para baixo pelo navegador.

Então, qndo o navegador chegar nas tags <script> dentro do <head>, ainda não temos nenhum html, e portanto, precisamos dizer que o nosso script precisa esperar o documento carregar, para só então começar a tentar ler o DOM.

Fazemos isso, assim:

``` js
window.onload = function(){

  }
```

ou seja, esperando o evento **.onload** do objeto **window**.

Quando então esse evento for disparado(o documento, imagens, css, scripts terminarem de carregar), disparamos uma function.

Olhando nosso HTML:

``` html
<ul id="fotos">
    <li><a href="images/01.jpg"><img src="images/thumbs/01.jpg" alt="Céu" /></a><p></p></li>
    <li><a href="images/02.jpg"><img src="images/thumbs/02.jpg" alt="Queda de agua" /></a><p></p></li>
```

Vemos que podemos limitar a ação do script, às imagens que estão dentro dos LIs, que estão dentro do UL#fotos:

``` js
var lis =  document.getElementById('fotos').getElementsByTagName('li');
```

com calma.

Criamos uma variavel **lis**, usando a palavra chave **var**.

Daí, atribuimos a essa variavel, o retorno do encadeamento.

``` js
document.getElementById('fotos').getElementsByTagName('li');
```

Apartir do objeto document, buscamos um elemento com id=&#8221;fotos&#8221;, dai então <u>dentro</u>, desse objeto que tinha id=&#8221;fotos&#8221;, <u>buscamos todos os elementos</u>, que tenham como tag name a string **li**.

Percorremos o DOM, e agora temos em **lis**, um array de objetos

``` js
alert( lis );//[object HTMLCollection]
```

, onde cada um é:

``` js
alert( lis[i] );//[object HTMLLIElement]
```

.

Basta iterar sob esse array:

``` js
for( var i=0; i<lis.length; i++ ){

    }
```

Lembrando que arrays em php, javascript, java.. começam na posição 0.(só tem uma linguagem que esqueci o nome que não é assim, começa no 1).

**lis.length**, nos retorna o número de elementos do nosso conjunto.

Nosso loop, vai percorrer da primeira posição, até a última. Bem simples.

Daí, só precisamos escrever no HTML.

Veja que tem um <p> ali estrategicamente posicionado para conter a legenda.

basta:

``` js
lis[i].getElementsByTagName( 'p' )[0].innerHTML
```

, atribuir à propriedade .innerHTML, do parágrafo, do nosso li corrente, oque queremos.

Veja que tem aquele [0], ali. Quer dizer que vamos trabalhar apenas com a primeira posição do array que getElementsByTagName() retornar.(mesmo que só haja um elemento, ele vai retornar um array com esse elemento).

De forma análoga, basta acessarmos o atributo .alt</strong>, das nossa imagem que está dentro do nosso li corrente:

``` js
lis[i].getElementsByTagName( 'img' )[0].alt
```

E está feito:

``` js
window.onload = function(){
    var lis =  document.getElementById('fotos').getElementsByTagName('li');

    for( var i=0; i<lis.length; i++ ){
      lis[i].getElementsByTagName( 'p' )[0].innerHTML = lis[i].getElementsByTagName( 'img' )[0].alt;
    }
  }
```

Opinem! mandem sugestões de tutoriais, scripts, críticas, ou algum ponto que não expliquei direito.

**TestPlan**

Notar que enqnto as imagens estão carregando, não existe nenhum texto embaixo de cada uma delas.

E abrindo o código fonte html gerado (Ctrl + U), também não tem nada ali dentro da tag p.

Assim que as imagens terminarem de carregar, vai aparecer a legenda.

<a href="http://wbruno.com.br/scripts/adicionar-legendas.html" target="_blank">Demonstração</a>
