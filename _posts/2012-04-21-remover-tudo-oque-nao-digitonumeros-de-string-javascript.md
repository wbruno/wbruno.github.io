---
id: 1968
title: Remover tudo oque não for dígito(numeros) de string com javascript
date: 2012-04-21T10:52:32+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1968
permalink: /expressao-regular/remover-tudo-oque-nao-digitonumeros-de-string-javascript/
dsq_thread_id:
  - "2100917724"
categories:
  - Expressão Regular
---
Uma simples expressão regular, e o método .replace() do javascript.

``` html
<script type="text/javascript"> type="text/javascript">
var str = 'capa1';
alert( str.replace(/[^\d]+/g,'') )
</script>```