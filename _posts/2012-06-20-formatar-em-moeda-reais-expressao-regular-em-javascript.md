---
id: 2058
title: Formatar em moeda reais com expressão regular em javascript
date: 2012-06-20T14:02:30+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=2058
permalink: /expressao-regular/formatar-em-moeda-reais-expressao-regular-em-javascript/
dsq_thread_id:
  - "2100759208"
categories:
  - Expressão Regular
tags:
  - máscara
---
Boas!

Fiz aqui rapidinho uma função <var>getMoney()</var> que recebe uma string no formato: **R$ 1.000,00** e retorna um inteiro, para podermos fazer contas em javascript.

Depois uma outra função <var>formatReal()</var> que recebe um inteiro e devolve o número formatado segundo a nossa moeda: Real.

Entrada:

``` js
console.log( formatReal( 1000 ) );
console.log( formatReal( 19990020 ) );
console.log( formatReal( 12006 ) );
console.log( formatReal( 111090 ) );
console.log( formatReal( 1111 ) );
console.log( formatReal( 120090 ) );
```

Saida:

``` js
10,00
199.900,20
120,06
1.110,90
11,11
1.200,90
```

Utilizei a função str.replace() nativa da linguagem javascript, e algumas expressões regulares.

Atualmente só formata até 999mil reais, não fiz a ER para colocar o ponto dos milhões.

``` html
<script type="text/javascript"> type="text/javascript">

var test = 'R$ 1.700,90';


function getMoney( str )
{
        return parseInt( str.replace(/[\D]+/g,'') );
}
function formatReal( int )
{
        var tmp = int+'';
        tmp = tmp.replace(/([0-9]{2})$/g, ",$1");
        if( tmp.length > 6 )
                tmp = tmp.replace(/([0-9]{3}),([0-9]{2}$)/g, ".$1,$2");

        return tmp;
}


var int = getMoney( test );
//alert( int );


console.log( formatReal( 1000 ) );
console.log( formatReal( 19990020 ) );
console.log( formatReal( 12006 ) );
console.log( formatReal( 111090 ) );
console.log( formatReal( 1111 ) );
console.log( formatReal( 120090 ) );
console.log( formatReal( int ) );


</script>
```
