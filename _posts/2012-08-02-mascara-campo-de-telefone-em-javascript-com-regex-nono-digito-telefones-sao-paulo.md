---
id: 2178
title: 'Mascara campo de telefone em javascript com regex - Nono dígito - Telefones São Paulo'
date: 2012-08-02T22:25:03+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=2178
permalink: /expressao-regular/mascara-campo-de-telefone-em-javascript-com-regex-nono-digito-telefones-sao-paulo/
dsq_thread_id:
  - "2100743227"
categories:
  - Expressão Regular
tags:
  - máscara
---
Boas!

Fiz uma rápida adaptação da **expressão regular**, usada na função **mtel()**. Que eu já havia postado aqui:

[https://wbruno.com.br/expressao-regular/diversas-mascaras-com-er/](https://wbruno.com.br/expressao-regular/diversas-mascaras-com-er/ "Mascaras em javascript com regex")

Aumentei o maxlenght de 14 para 15.

``` html
<html>
<head>
    <title>Mascara Telefone</title>
    <script type="text/javascript" src="mtel.js"></script>

</head>
<body>

    <input type="text" name="telefone" onkeyup="mascara( this, mtel );" maxlength="15" />

</body>
</html>
```

E o mtel.js

``` js
/* Máscaras ER */
function mascara(o,f){
    v_obj=o
    v_fun=f
    setTimeout("execmascara()",1)
}
function execmascara(){
    v_obj.value=v_fun(v_obj.value)
}
function mtel(v){
    v=v.replace(/\D/g,"");             //Remove tudo o que não é dígito
    v=v.replace(/^(\d{2})(\d)/g,"($1) $2"); //Coloca parênteses em volta dos dois primeiros dígitos
    v=v.replace(/(\d)(\d{4})$/,"$1-$2");    //Coloca hífen entre o quarto e o quinto dígitos
    return v;
}
```

Alterei a segunda expressão regular, para funcionar de forma invertida. De trás para frente.

Contar os 4 últimos dígitos finais, e colocar o hífen antes deles. Deixando assim, o DD quatro ou cinco dígitos, depois o hífen, e os próximos quatro dígitos.

Usou ? gostou ?

Comente!!

## &#8212; update &#8212;

Apenas para alertar que a forma acima, não é a melhor maneira de implementar.

Devemos separar as camadas, e deixar a chamada do script do lado do js. Dessa forma aqui:

``` html
<html>
<head>
    <title>Mascara Telefone</title>
<script type="text/javascript">
/* Máscaras ER */
function mascara(o,f){
    v_obj=o
    v_fun=f
    setTimeout("execmascara()",1)
}
function execmascara(){
    v_obj.value=v_fun(v_obj.value)
}
function mtel(v){
    v=v.replace(/\D/g,"");             //Remove tudo o que não é dígito
    v=v.replace(/^(\d{2})(\d)/g,"($1) $2"); //Coloca parênteses em volta dos dois primeiros dígitos
    v=v.replace(/(\d)(\d{4})$/,"$1-$2");    //Coloca hífen entre o quarto e o quinto dígitos
    return v;
}
function id( el ){
  return document.getElementById( el );
}
window.onload = function(){
  id('telefone').onkeyup = function(){
    mascara( this, mtel );
  }
}
</script>

</head>
<body>

    <input type="text" name="telefone" id="telefone" maxlength="15" />

</body>
</html>
```
