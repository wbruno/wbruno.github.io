---
id: 2930
title: 'Exemplo regex para casar um padrão de link - javascript'
date: 2013-03-21T11:52:49+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=2930
permalink: /expressao-regular/exemplo-regex-para-casar-um-padrao-de-link-javascript/
categories:
  - Expressão Regular
---
Exemplo básico de uso do método [b].test()[/b] do objeto Regex.

Vou casar todos os links, que terminem em 32 caracteres(letras ou números).

``` js
<a href="http://www.site.com.br/caminho/pasta/c8f388d1917311e2a180000c29d05625">sim</a>
<a href="http://www.site.com.br/caminho/pasta/c8f388d1917311e2a180000c29d05625">sim</a>
<a href="http://www.site.com.br/caminho/pasta/c8f388d1917311e2a180000c29d05625aa">nao</a>
<a href="http://www.site.com.br/caminho/pasta/c8f388d1917311e2a180000c29d05625">sim</a>

<a href="http://www.site.com.br">nao</a>

<a href="http://www.site.com.br/caminho/pasta/c8f388d1917311e2a180000c29d05625aa">nao</a>
<a href="http://www.site.com.br/caminho/pasta/123412341234aaaabbbbccccddddeeee">sim</a>


<style>
.t { color: #f00; }
</style>
<script>
  var as = document.getElementsByTagName('a'),
    max = as.length;

  while(max--){
    var er = /\/[a-z0-9]{32}$/gi;

    if(er.test(as[max].href)){
      as[max].className = 't';
    }
  }
</script>
```

Mais um código que fiz para o iMasters, e resolvi postar aqui. =)
