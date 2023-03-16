---
id: 2931
title: 'Máscara cartão de crédito com javascript e expressão regular &#8211; regex'
date: 2013-03-25T10:35:32+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2931
permalink: /expressao-regular/mascara-cartao-de-credito-com-javascript-e-expressao-regular-regex/
dsq_thread_id:
  - "2102815008"
categories:
  - Expressão Regular
tags:
  - máscara
---
EU já havia postado [diversas máscaras com javascript e regex](http://wbruno.com.br/2011/03/12/diversas-mascaras-com-er/), e hoje um cara no fórum pediu uma máscara para **cartão de crédito**.

É bem simples, 4 grupos de números separados por espaços.&#8221;9999 9999 9999 9999&#8243;.
  
Eu odeio os plugins de máscaras, pois eles sempre dão algum tipo de problema, como impedir usar backspace, o backspace funcionar até se tiver readonly, comer números, ser impossível editar corretamente, jogar o cursor no lugar errado..

Então eu sempre uso essas máscaras com expressões regulares. Funcionam muito bem, são super crossbrowsers, e tem ótima performance.

``` html
<html>
<head>
    <title>Mascara Cartão de Crédito</title>
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
function mcc(v){
    v=v.replace(/\D/g,"");
    v=v.replace(/^(\d{4})(\d)/g,"$1 $2");
    v=v.replace(/^(\d{4})\s(\d{4})(\d)/g,"$1 $2 $3");
    v=v.replace(/^(\d{4})\s(\d{4})\s(\d{4})(\d)/g,"$1 $2 $3 $4");
    return v;
}
function id( el ){
  return document.getElementById( el );
}
window.onload = function(){
  id('cc').onkeypress = function(){
    mascara( this, mcc );
  }
}
</script>

</head>
<body>

    <input type="tel" name="cc" id="cc" maxlength="19" />

</body>
</html>
```

Comente se vc usar também.