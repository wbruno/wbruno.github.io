---
id: 3114
title: Adicionar/Remover campos com javascript
date: 2013-10-29T15:36:49+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=3114
permalink: /javascript-puro/adicionarremover-campos-com-javascript/
dsq_thread_id:
  - "2103125749"
categories:
  - Javascript
tags:
  - formulário
---
Rotina bem conhecida e muito usada. Mas implementei de uma forma que ao remover campos já adicionados, os demais não sejam apagados.

``` html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
<style>
label { display: block; }
</style>
</head>
<body>

<select name="children-qnt" id="children-qnt">
  <option value="0">0</option>
  <option value="1">1</option>
  <option value="2">2</option>
  <option value="3">3</option>
  <option value="4">4</option>
  <option value="5">5</option>
  <option value="6">6</option>
</select>
<fieldset id="children">

</fieldset><!-- #children -->

<script type="text/javascript" src="http://code.jquery.com/jquery-1.10.2.min.js"></script>
<script type="text/javascript">
var $chidrenQnt = jQuery('#children-qnt'),
  $children = jQuery('#children');



var Children = {};
Children.container = $children;
Children.add = function(i) {
  while (i--) {
    Children.container.append('<label>idade: <input type="text" name="" /></label>');
  }
}
Children.remove = function(i) {
  while (i--) {
    Children.container.find('label:last').remove();
  }
}


$chidrenQnt.on('change', function(){
  var $this = jQuery(this),
    i = $this.val(),
    qnt = $children.find('label').length;


  if (qnt > i) {
    Children.remove(qnt - i);
  }
  if (qnt < i) {
    Children.add(i - qnt);
  }
});


</script>

</body>
</html>
```
