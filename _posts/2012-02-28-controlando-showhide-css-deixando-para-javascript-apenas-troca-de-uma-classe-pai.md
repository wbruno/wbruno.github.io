---
id: 1803
title: 'Controlando show/hide com css &#8211; Deixando para o javascript apenas a troca de uma classe pai'
date: 2012-02-28T14:43:16+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1803
permalink: /javascript-puro/controlando-showhide-css-deixando-para-javascript-apenas-troca-de-uma-classe-pai/
dsq_thread_id:
  - "2101063004"
categories:
  - Javascript
---
Boas =)

A minha proposta aqui, é controlar toda a lógica do show/hide com css.
  
Em vez de fazermos malabarismos com coisas como:
  
<!--more-->

``` js
document.getElementById("Carro").className = "invisivel";
        document.getElementById("Moto").className = "invisivel";
        document.getElementById("Pesados").className = "invisivel";
        document.getElementById("Agrícolas").className = "invisivel";
        document.getElementById("selecione").className = "invisivel";
        document.getElementById(div).className = "visivel";
```

E ai, qndo tiver q mostrar mais de um elemento a cada option do select, recorrer a colocar mais linhas/parâmetros no js.
  
O javascript que proponho é o seguinte:

``` js
function id( obj ){ return document.getElementById( obj ); }
window.onload = function(){
  id('escolha').onchange = function(){
    id('pai').className = this.value;
  }
}
```

E conforme queiramos mais elementos a serem mostrados, ou mais regras, não temos que alterar absolutamente nada no js.
  
Apenas no html, e no css.
  
Veja que toda a lógica de mostrar/esconder, está no css:

``` css
p, #lista li { display: none; }

.carros #palio, 
.carros #punto,
.carros #gol,
.carros #volks { display: block; }

.animais #gato, 
.animais #cao,
.animais #vet { display: block; }
/* deixei separado apenas para facilitar o entendimento */
.linguagens #ajax, 
.linguagens #js,
.linguagens #css,
.linguagens #programador { display: block; }
```

A primeira regra css, esconde tudo.
  
As demais, vão dando block, conforme uma classe pai. Exatamente a que estamos alterando via js.

É isso. O que vc acha dessa abordagem ?

``` html
<html>
<head>
  <title>Show/Hide com css</title>
<script type="text/javascript">
function id( obj ){ return document.getElementById( obj ); }
window.onload = function(){
  id('escolha').onchange = function(){
    id('pai').className = this.value;
  }
}
</script>
<style type="text/css">
p, #lista li { display: none; }


.carros #palio, 
.carros #punto,
.carros #gol,
.carros #volks { display: block; }

.animais #gato, 
.animais #cao,
.animais #vet { display: block; }

.linguagens #ajax, 
.linguagens #js,
.linguagens #css,
.linguagens #programador { display: block; }

</style>
</head>
<body>
  <select name="escolha" id="escolha">
    <option value="">Esconder todos</option>
    <option value="carros">Carros</option>
    <option value="animais">Animais</option>
    <option value="linguagens">Linguagens</option>
  </select>
  
  <div id="pai">
    <ul id="lista">
      <li id="palio">Palio</li>
      <li id="punto">Punto</li>
      <li id="gol">Gol</li>
      
      <li id="gato">Gato</li>
      <li id="cao">Cão</li>
      
      <li id="ajax">AJAX</li>
      <li id="js">JS</li>
      <li id="css">CSS</li>
    </ul><!-- /lista -->
    
    <p id="volks">Volks</p>
    
    <p id="vet">Veterinária</p>
    
    <p id="programador">Programador</p>
  </div>
</body>
</html>
```

## <a href="http://wbruno.com.br/scripts/showhidecss.html" target="_blank">Demonstração</a>