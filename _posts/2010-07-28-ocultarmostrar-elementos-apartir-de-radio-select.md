---
id: 68
title: Ocultar/Mostrar elementos apartir de radio select
date: 2010-07-28T01:05:36+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=68
permalink: /javascript-puro/ocultarmostrar-elementos-apartir-de-radio-select/
dsq_thread_id:
  - "2100934960"
categories:
  - Javascript
---
**16/04/2015** &#8211; Atualizei o código em JavaScript puro e jQuery para mostrar assim que carregar a página.
  
Então se o radio ou o select já tiver algum valor selecionado, o script lê esse valor e já mostra o elemento correspondente ao carregar a página.

## Select

``` html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>

<script type="text/javascript">
function id(el) {
  return document.getElementById(el);
}
function mostra(element) {
  if (element.value) {
    id(element.value).style.display = 'block';
  }
}
function esconde_todos($element, tagName) {
  var $elements = $element.getElementsByTagName(tagName),
      i = $elements.length;
  while(i--) {
    $elements[i].style.display = 'none';
  }
}
window.addEventListener('load', function() {
  var $Masculino = id('Masculino'),
      $Feminino = id('Feminino'),
      $sexo  = id('sel-sexo');

  //mostrando no onload da página
  esconde_todos(id('palco'), 'div');
  mostra($sexo);

  //mostrando ao mudar o select
  $sexo.addEventListener('change', function() {
    esconde_todos(id('palco'), 'div');
    mostra(this);
  });
});
</script>
</head>
<body>
  <select name="sel-sexo" id="sel-sexo">
    <option value="">--</option>
    <option value="Feminino">Feminino</option>
    <option value="Masculino">Masculino</option>
  </select>

  <div id="palco">
    <div id="Masculino">Seu sexo é Masculino!</div>
    <div id="Feminino">Seu sexo é Feminino!</div>
  </div>

</body>
</html>
```

## Radio

``` html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>

<script type="text/javascript">
function id(el) {
  return document.getElementById(el);
}
function mostra(element) {
  if (element) {
    id(element.value).style.display = 'block';
  }
}
function esconde_todos($element, tagName) {
  var $elements = $element.getElementsByTagName(tagName),
      i = $elements.length;
  while(i--) {
    $elements[i].style.display = 'none';
  }
}
window.addEventListener('load', function() {
  var $Masculino = id('Masculino'),
      $Feminino = id('Feminino'),
      $sexo  = id('sel-sexo');

  //mostrando no onload da página
  esconde_todos(id('palco'), 'div');
  mostra(document.querySelector('input[name="rd-sexo"]:checked'));


  //mostrando ao clicar no radio
  var $radios = document.querySelectorAll('input[name="rd-sexo"]');
  $radios = [].slice.call($radios);

  $radios.forEach(function($each) {
    $each.addEventListener('click', function() {
      esconde_todos(id('palco'), 'div');
      mostra(this);
    });
  });
});
</script>
</head>
<body>
<label>
  <label><input type="radio" name="rd-sexo" value="Feminino" />Feminino</label>
  <label><input type="radio" name="rd-sexo" value="Masculino" />Masculino</label>

  <div id="palco">
    <div id="Masculino">Seu sexo é Masculino!</div>
    <div id="Feminino">Seu sexo é Feminino!</div>
  </div>


</body>
</html>
```

### No github:

<https://github.com/wbruno/examples>

## Com jquery

<http://wbruno.github.io/examples/select-radio/radio-jquery.html>
  
<http://wbruno.github.io/examples/select-radio/select-jquery.html>