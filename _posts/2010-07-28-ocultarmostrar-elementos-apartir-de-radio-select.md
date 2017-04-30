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

<pre name="code" class="html">&lt;!DOCTYPE html>
&lt;html lang="en">
&lt;head>
  &lt;meta charset="UTF-8">
  &lt;title>Document&lt;/title>

&lt;script type="text/javascript">
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
&lt;/script>
&lt;/head>
&lt;body>
  &lt;select name="sel-sexo" id="sel-sexo">
    &lt;option value="">--&lt;/option>
    &lt;option value="Feminino">Feminino&lt;/option>
    &lt;option value="Masculino">Masculino&lt;/option>
  &lt;/select>

  &lt;div id="palco">
    &lt;div id="Masculino">Seu sexo é Masculino!&lt;/div>
    &lt;div id="Feminino">Seu sexo é Feminino!&lt;/div>
  &lt;/div>

&lt;/body>
&lt;/html>
</pre>

## Radio

<pre>&lt;!DOCTYPE html>
&lt;html lang="en">
&lt;head>
  &lt;meta charset="UTF-8">
  &lt;title>Document&lt;/title>

&lt;script type="text/javascript">
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
&lt;/script>
&lt;/head>
&lt;body>
&lt;label>
  &lt;label>&lt;input type="radio" name="rd-sexo" value="Feminino" />Feminino&lt;/label>
  &lt;label>&lt;input type="radio" name="rd-sexo" value="Masculino" />Masculino&lt;/label>

  &lt;div id="palco">
    &lt;div id="Masculino">Seu sexo é Masculino!&lt;/div>
    &lt;div id="Feminino">Seu sexo é Feminino!&lt;/div>
  &lt;/div>


&lt;/body>
&lt;/html>
</pre>

### No github:

<https://github.com/wbruno/examples>

## Com jquery

<http://wbruno.github.io/examples/select-radio/radio-jquery.html>
  
<http://wbruno.github.io/examples/select-radio/select-jquery.html>