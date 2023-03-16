---
id: 63
title: Somar inputs dentro de fieldset javascript
date: 2010-07-23T23:54:41+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=63
permalink: /javascript-puro/somar-inputs-dentro-de-fieldset-javascript/
categories:
  - Javascript
tags:
  - cálculo
---
``` html
<html>
<head>
<script type="text/javascript">
  function id( el ){
    return document.getElementById( el );
  }
  function soma(){
    var inputs = id('campos').getElementsByTagName('input');

    var soma =0;
    for( var i=0; i<inputs.length; i++ ){
      soma += parseInt( inputs[i].value );
    }
    id('resultado').value = soma;
  }
  window.onload = function(){
    id('somar').onclick = function(){
      soma();
    }
  }
  </script>
</head>
<body>
  <form action="" method="post">
    <fieldset id="campos">
      <label><input type="text" name="valor[]" value="2" /></label>
      <label><input type="text" name="valor[]" value="5" /></label>
      <label><input type="text" name="valor[]" value="8" /></label>
      <label><input type="text" name="valor[]" value="9" /></label>
      <label><input type="text" name="valor[]" value="1" /></label>
    </fieldset>

    <input type="button" name="somar" id="somar" value="Somar" />
    <label>Total Soma: <input type="text" name="resultado" id="resultado" /></label>
  </form>
</body>
</html>?
```