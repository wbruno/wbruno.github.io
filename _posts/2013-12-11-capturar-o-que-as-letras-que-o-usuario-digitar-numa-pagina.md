---
id: 3147
title: Capturar o que as letras que o usuário digitar numa página
date: 2013-12-11T13:58:39+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3147
permalink: /javascript-puro/capturar-o-que-as-letras-que-o-usuario-digitar-numa-pagina/
dsq_thread_id:
  - "2105245869"
categories:
  - Javascript
---
```<div id="t"></div>
<script>
var keyTable = {
    '65': 'a',
    '66': 'b',
    '67': 'c',
    '68': 'd',
    '69': 'e',
    '70': 'f',
    '71': 'g',
    '72': 'h',
    '73': 'i',
    '74': 'j',
    '75': 'k',
    '76': 'l',
    '77': 'm',
    '78': 'n',
    '79': 'o',
    '80': 'p',
    '81': 'q',
    '82': 'r',
    '83': 's',
    '84': 't',
    '85': 'u',
    '86': 'v',
    '87': 'w',
    '88': 'x',
    '89': 'y',
    '90': 'z'
}
var userTyped = '';
document.addEventListener("keyup", function(e){
    if (keyTable[e.keyCode] !== undefined ) {
        userTyped += keyTable[e.keyCode];
    }

    document.getElementById("t").innerHTML = userTyped;
});
</script>
```

Bem simples, só ouvi o evento **onkeyup**, e fiz uma tabela para &#8220;traduzir&#8221; o <var>keyCode</var> para a letra correspondente.