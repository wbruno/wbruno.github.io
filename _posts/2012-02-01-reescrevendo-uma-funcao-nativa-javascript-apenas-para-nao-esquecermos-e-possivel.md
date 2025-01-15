---
id: 1765
title: 'Reescrevendo uma função nativa do javascript - apenas para não esquecermos que é possível.'
date: 2012-02-01T19:21:54+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1765
permalink: /javascript-puro/reescrevendo-uma-funcao-nativa-javascript-apenas-para-nao-esquecermos-e-possivel/
dsq_thread_id:
  - "2103229244"
categories:
  - Javascript
---
``` html
<script type="text/javascript"> type="text/javascript">
var _write = document.write;
document.write('<br />1');//vai funcionar normal

document.write = function(){
        //não faz nada
}
document.write('<br />2');//não vai funcionar
document.write('<br />2');//não vai funcionar
document.write('<br />2');//não vai funcionar
document.write('<br />2');//não vai funcionar
document.write('<br />2');//não vai funcionar


document.write = _write;
document.write('<br />3');//voltou a funcionar
</script>
```
