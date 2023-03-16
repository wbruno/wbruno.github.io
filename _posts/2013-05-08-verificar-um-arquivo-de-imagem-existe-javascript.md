---
id: 2954
title: 'Verificar se um arquivo de imagem existe &#8211; JavaScript'
date: 2013-05-08T10:10:01+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2954
permalink: /ajax/verificar-um-arquivo-de-imagem-existe-javascript/
dsq_thread_id:
  - "2102726955"
categories:
  - AJAX
---
Dado um arquivo de imagem, como verificar se ele existe usando apenas javascript ?

Eu consegui pensar em pelo menos três formas de fazer isso.
  
<!--more-->

## Verificando com AJAX

<pre class="javascript"><script type="text/javascript">
function is_img(file) {
  var ajax = new XMLHttpRequest();

  ajax.open("GET",file,true);
  ajax.send();

  ajax.onreadystatechange = function() {
    if (ajax.readyState == 4){
      var jpg = ajax.responseText;

      if(ajax.status===200) {
        console.log("A imagem " + file + " existe");
      } else {
        console.log("A imagem " + file + " NAO existe");
      }
    }
  }
}
is_img("imagem-garfield.jpg");
is_img("imagem-garfield-2.jpg");
</script>
```

A propriedade <var>status</var> do objeto ajax existe exatamente para isso. Caso não exista ela retorna 404, caso exista retornará 200, ou então 304(not modified) dependendo de como você serve imagens com o teu servidor.

## Verificando com new Image();

<pre class="javascript"><script type="text/javascript">
function is_img(file) {
  var img = new Image();
  img.src = file;
  img.onload = function() {
    console.log("A imagem " + file + " existe");
  }
  img.onerror = function() {
    console.log("A imagem " + file + " NAO existe");
  }
}
is_img("imagem-garfield.jpg");
is_img("imagem-garfield-2.jpg");
</script>
```

Outra possibilidade é usar aquele truque que conhecemos para fazer preload de arquivos de imagem, usando o objeto <var>Image()</var>

Aqui é bem simples, se a imagem responder no evento <var>onload()</var>, então ela existe, caso não, disparará o evento onerror, ai sei que deu algo errado.

## Verificar com document.createElement

Aqui o truque para saber se o arquivo de imagem existe ou não, é o mesmo do método acima. Usando os eventos <var>onload</var>, e <var>onerror</var>. Porém o resource agora é criado com um elemento imagem, e não com o objeto.

<pre class="javascript"><script type="text/javascript">
function is_img(file) {
  var img = document.createElement('img');
  img.src = file;

  img.onload = function() {
    console.log("A imagem " + file + " existe");
  }
  img.onerror = function() {
    console.log("A imagem " + file + " NAO existe");
  }

}
is_img("imagem-garfield.jpg");
is_img("imagem-garfield-2.jpg");
</script>
```