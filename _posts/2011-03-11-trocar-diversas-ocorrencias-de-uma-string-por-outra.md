---
id: 175
title: Trocar diversas ocorrências de uma string por outra
date: 2011-03-11T21:44:01+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=175
permalink: /javascript-puro/trocar-diversas-ocorrencias-de-uma-string-por-outra/
categories:
  - Javascript
---
Bom, nunca se sabe se pode ser útil a alguém, portanto, não vou menosprezar esse post que fiz no iMasters, deixo aqui registrado como usar o modificador /g com o metodo replace

``` html
<script type="text/javascript"> type="text/javascript">
        var str = 'lucassssssssssssss';

        alert( 'string ANTES do replace: '+str );//lucassssssssssssss
        alert( 'strong DEPOIS do replace: '+str.replace( /s/g, 'o' ) );///lucaoo...

</script>
```
