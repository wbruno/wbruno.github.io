---
id: 3290
title: Upload de arquivos e dados com ajax
date: 2015-02-26T13:44:39+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3290
permalink: /ajax/upload-de-arquivos-e-dados-com-ajax/
categories:
  - AJAX
tags:
  - ajax
  - php
---
Ajax não envia arquivos.
  
Ajax não envia arquivos.

Isso sempre foi verdade até a chegada de algumas APIs JavaScript junto com o html5.
  
<!--more-->

Ajax nada mais é do que uma requisição http feita pelo objeto XMLHttpRequest, e o retorno é devolvido diretamente ao javascript, assim não tendo o famoso e as vezes indesejado &#8220;refresh&#8221;.

Irei utilizar como base o código disponibilizado na MDN, no tutorial [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData). Esta serve apenas para enviar dados em formato: chave/valor, ou seja, os nossos inputs.

[Código completo no github](http://github.com/wbruno/examples/tree/gh-pages/upload-ajax/)

**index.html**

``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <title>Upload ajax</title>
</head>
<body>

<form action="upload.php" method="post" id="upload">
  <input type="file" name="file" id="file" accept="image/*" />
  <input type="text" name="name" value="wBruno" />
  <input type="submit" value="Send!" />
</form>

<div id="preview"></div>

<script>
var $formUpload = document.getElementById('upload'),
    $preview = document.getElementById('preview'),
    i = 0;

$formUpload.addEventListener('submit', function(event){
  event.preventDefault();

  var xhr = new XMLHttpRequest();

  xhr.open("POST", $formUpload.getAttribute('action'));

  var formData = new FormData($formUpload);
  formData.append("i", i++);
  xhr.send(formData);

  xhr.addEventListener('readystatechange', function() {
    if (xhr.readyState === 4 && xhr.status == 200) {
      var json = JSON.parse(xhr.responseText);

      if (!json.error && json.status === 'ok') {
        $preview.innerHTML += '<br />Enviado!!';
      } else {
        $preview.innerHTML = 'Arquivo não enviado';
      }

    }
  });

  xhr.upload.addEventListener("progress", function(e) {
    if (e.lengthComputable) {
      var percentage = Math.round((e.loaded * 100) / e.total);
      $preview.innerHTML = String(percentage) + '%';
    }
  }, false);

  xhr.upload.addEventListener("load", function(e){
    $preview.innerHTML = String(100) + '%';
  }, false);

}, false);

</script>

</body>
</html>
```