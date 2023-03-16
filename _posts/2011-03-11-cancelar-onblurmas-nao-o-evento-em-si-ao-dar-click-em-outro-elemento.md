---
id: 173
title: 'Cancelar &#039;onblur&#039;(mas não o evento em si), ao dar click em outro elemento'
date: 2011-03-11T21:36:37+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=173
permalink: /javascript-puro/cancelar-onblurmas-nao-o-evento-em-si-ao-dar-click-em-outro-elemento/
categories:
  - Javascript
---
Boas galera!

mais uma dúvida que surgiu no iMasters.

A melhor forma que consegui pensar para resolver essa situação, foi usando um <cite>setTimeout</cite>, para atrasar o disparo da função invocada pelo evento onblur.
  
Veja, não dá para &#8216;cancelar o evento&#8217;. Quando vc tirar o foco do input, para clicar no button, irá acontecer instantaneamente o evento **onblur do input**.

Rodem este script, para entenderem a situação:

``` html
<script type="text/javascript"> type="text/javascript">
function id( el ){
        return document.getElementById( el );
}
function escreve(){
        id('result').innerHTML += i+'<br />';
        i++;
}
var i = 0;
var itv = 0;
window.onload = function(){
        id('q').onblur = function(){
                window.clearInterval( itv );
                itv = window.setInterval( escreve, 200 );
        }
        id('ok').onclick = function(){
                id('result').innerHTML += 'cancelar ação<br />';
                window.clearInterval( itv );
        }
}
</script>

<input type="text" name="q" id="q" />
<input type="button" name="ok" value="Ok" id="ok" />

<div id="result"></div>
```

basta comentar esta linha:

``` js
window.clearInterval( itv );
```

para entender oque acontece.

script final, então, para &#8216;cancelar o evento&#8217;:

``` js
window.onload = function(){

        id('q').focus();

        id('q').onblur = function(){
                tot = window.setTimeout( escreve, 500 );
        }
        id('cboption').onclick = function(){
                id('result').innerHTML += 'cancelar ação<br />';
                window.clearTimeout( tot );
        }
}
```