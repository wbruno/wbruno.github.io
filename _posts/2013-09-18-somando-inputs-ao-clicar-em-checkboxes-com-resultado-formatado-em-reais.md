---
id: 3083
title: Somando inputs ao clicar em checkboxes, com resultado formatado em reais
date: 2013-09-18T14:29:03+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3083
permalink: /javascript-puro/somando-inputs-ao-clicar-em-checkboxes-com-resultado-formatado-em-reais/
dsq_thread_id:
  - "2104187898"
categories:
  - Javascript
tags:
  - formulário
---
[<img src="/wp-content/uploads/2013/09/a1.png" alt="a" width="420" height="263" class="aligncenter size-full wp-image-3089" />](/wp-content/uploads/2013/09/a1.png)

Imagine uma lista de checkboxes. Cada um possui um valor. Ao clicar em cima deles, vai somando em um outro input text todos os checks que estiverem marcados. E ao desmarcar o valor é subtraido.

<!--more-->

## Demonstração

Veja no meu github a demonstração do código abaixo: <http://wbruno.github.io/checkSum/>

## Código

<pre class="javascript">&lt;!doctype html>
&lt;html lang="en">
&lt;head>
    &lt;meta charset="UTF-8">
    &lt;title>Document&lt;/title>
&lt;style>
label { display: block; }
&lt;/style>
&lt;/head>
&lt;body>

    &lt;label>1,00 &lt;input type="checkbox" name="ch[]" value="1,00" />&lt;/label>
    &lt;label>2,00 &lt;input type="checkbox" name="ch[]" value="2,00" />&lt;/label>
    &lt;label>3,00 &lt;input type="checkbox" name="ch[]" value="3,00" />&lt;/label>
    &lt;label>4,00 &lt;input type="checkbox" name="ch[]" value="4,00" />&lt;/label>
    &lt;label>5,00 &lt;input type="checkbox" name="ch[]" value="5,00" />&lt;/label>
    &lt;label>6,00 &lt;input type="checkbox" name="ch[]" value="6,00" />&lt;/label>
    &lt;label>7,00 &lt;input type="checkbox" name="ch[]" value="7,00" />&lt;/label>
    &lt;label>8,00 &lt;input type="checkbox" name="ch[]" value="8,00" />&lt;/label>
    &lt;label>9,00 &lt;input type="checkbox" name="ch[]" value="9,00" />&lt;/label>
    &lt;label>10,00 &lt;input type="checkbox" name="ch[]" value="10,00" />&lt;/label>

    &lt;label>Resultado &lt;input type="text" name="result" id="result" value="R$ 0,00" />&lt;/label>

&lt;script>
String.prototype.formatMoney = function() {
    var v = this;

    if(v.indexOf('.') === -1) {
        v = v.replace(/([\d]+)/, "$1,00");
    }

    v = v.replace(/([\d]+)\.([\d]{1})$/, "$1,$20");
    v = v.replace(/([\d]+)\.([\d]{2})$/, "$1,$2");
    v = v.replace(/([\d]+)([\d]{3}),([\d]{2})$/, "$1.$2,$3");

    return v;
};
String.prototype.toFloat = function() {
    var v = this;

    if (!v) return 0;
    return parseFloat(v.replace(/[\D]+/g, '' ).replace(/([\d]+)(\d{2})$/, "$1.$2"));
};
(function(){
    "use strict";

    var $chs = document.querySelectorAll('input[name="ch[]"]'),
        $result = document.getElementById('result'),
        chsArray = Array.prototype.slice.call($chs);

    chsArray.forEach(function(element, index, array){
        element.addEventListener("click", function(){
            var v = this.value,
                result = 0;
            v = v.toFloat();

            if (this.checked === true) {
                result = $result.value.toFloat() + parseFloat(v);
            } else {
                result = $result.value.toFloat() - parseFloat(v);
            }

            $result.value = "R$ " + String(result).formatMoney();
        });
    });


}());
&lt;/script>
&lt;/body>
&lt;/html>
</pre>
