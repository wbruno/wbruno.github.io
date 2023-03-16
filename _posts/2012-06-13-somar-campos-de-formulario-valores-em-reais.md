---
id: 2053
title: Somar campos de formulário com valores em Reais em javascript
date: 2012-06-13T15:13:42+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2053
permalink: /javascript-puro/somar-campos-de-formulario-valores-em-reais/
dsq_thread_id:
  - "2100774281"
categories:
  - Javascript
tags:
  - cálculo
---
Opa!

Apenas para deixar registrado por aqui, um script bem antigo meu que fiz para o iMasters.
  
Um formulário, fazendo operações básicas de soma, e subtração com valores em reais.

O único ponto que &#8220;confunde&#8221; os iniciantes, é que o sistema decimal americano usa o ponto no lugar da nossa vírgula, e por isso, preciso &#8220;converter&#8221; os valores antes de somar.

``` html
<html>
<head>
<script type="text/javascript">
function id( el ){
        return document.getElementById( el );
}
function getMoney( el ){
        var money = id( el ).value.replace( ',', '.' );
        return parseFloat( money )*100;
}
function soma()
{
        var total = getMoney('campo1')+getMoney('campo2')+getMoney('campo3');
        id('campo4').value = 'R$ '+total/100;
}
</script>
</head>
<body>
        <form action="" method="">
                <input name="campo1" id="campo1" value="25,60" /><br />
                <input name="campo2" id="campo2" value="5,15" /><br />
                <input name="campo3" id="campo3" value="2,63" /><br />
                <input name="campo4" readonly="readonly" id="campo4" /><br />
                <input type="button" onclick="soma()" value="Soma de Valores" />
        </form>
</body>
</html>

```

Original:
  
<a href="http://forum.imasters.com.br/topic/383476-soma-de-campo-em-r/page__view__findpost__p__1493512" el="nofollow">http://forum.imasters.com.br/topic/383476-soma-de-campo-em-r/page__view__findpost__p__1493512</a>