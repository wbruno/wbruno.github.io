---
id: 206
title: Cálculo simples entre inputs, resposta em outro
date: 2011-03-12T00:28:56+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=206
permalink: /javascript-puro/calculo-simples-entre-inputs-resposta-em-outro/
dsq_thread_id:
  - "2101003889"
categories:
  - Javascript
tags:
  - cálculo
---
<pre name="code" class="javascript">&lt;!DOCTYPE html>
&lt;html lang="en">
&lt;head>
  &lt;meta charset="UTF-8">
  &lt;title>Document&lt;/title>
&lt;/head>
&lt;body>
  &lt;form action="" method="post">
    Valor Unitário: &lt;input type="text" name="valor_unitario" id="valor_unitario" />
    Quantidade: &lt;input type="text" name="qnt" id="qnt" value="0" />
    Total: &lt;input type="text" name="total" id="total" readonly="readonly" />
  &lt;/form>

&lt;script type="text/javascript">
function id(el) {
  return document.getElementById( el );
}
function total( un, qnt ) {
  return parseFloat(un.replace(',', '.'), 10) * parseFloat(qnt.replace(',', '.'), 10);
}
window.onload = function() {
  id('valor_unitario').addEventListener('keyup', function() {
    var result = total( this.value , id('qnt').value );
    id('total').value = String(result.toFixed(2)).formatMoney();
  });

  id('qnt').addEventListener('keyup', function(){
    var result = total( id('valor_unitario').value , this.value );
    id('total').value = String(result.toFixed(2)).formatMoney();
  });
}

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
&lt;/script>

&lt;/body>
&lt;/html>

</pre>

## Em funcionamento

<http://wbruno.github.io/examples/calc-simples/>

**update**
  
2015-05-12 => Formatar em moeda o total. Utilizar addEventListener
  
2015-05-13 => .toFixed(2) para evitar dízimas