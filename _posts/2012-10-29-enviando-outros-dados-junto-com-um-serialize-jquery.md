---
id: 2815
title: 'Enviando outros dados junto com um .serialize() - jQuery'
date: 2012-10-29T18:34:41+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2815
permalink: /jquery/enviando-outros-dados-junto-com-um-serialize-jquery/
dsq_thread_id:
  - "2100900435"
categories:
  - jQuery
---
Opa! Apareceu essa dúvida no fórum hoje.

Note que o retorno do serialize() é apenas uma string. Uma simples string.

Descobri isso assim:

``` html
typeof $form.serialize();
```

Logo, se quero enviar outros dados junto com estes, então só preciso concatenar nessa string:

``` html
<script type="text/javascript"> type="text/javascript" src="http://code.jquery.com/jquery-1.8.2.min.js"></script>
<script type="text/javascript">
jQuery(document).ready(function(){
    var $form = jQuery('#form'),
    data = $form.serialize();



    console.log( data+'&a5=v5&a6=v6' );

});
</script>

<form action="" id="form">
    <input type="text" name="a1" value="v1" />
    <input type="text" name="a2" value="v2" />
    <input type="text" name="a3" value="v3" />
    <input type="text" name="a4" value="v4" />
</form>
```
Simples ne?! nada de desespero.. só entender oque temos em mãos e fazer.
