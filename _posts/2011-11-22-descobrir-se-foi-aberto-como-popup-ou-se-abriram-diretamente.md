---
id: 1606
title: Descobrir se foi aberto como popup, ou se abriram diretamente.
date: 2011-11-22T19:06:42+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1606
permalink: /javascript-puro/descobrir-se-foi-aberto-como-popup-ou-se-abriram-diretamente/
dsq_thread_id:
  - "2102129081"
categories:
  - Javascript
---
Dúvida rápida no fórum..

Será que é possível saber, se um documento foi aberto diretamente ? ou se ele foi aberto &#8216;como popup&#8217; ?

<!--more-->

**b.html**

``` html
<script type="text/javascript"> type="text/javascript">
alert( window.opener );
</script>
```
Qndo acessarmos diretamente esse arquivo, o alert irá mostrar: **null** (digitando na url, ou copiando e colando daqui)

<u>http://wbruno.com.br/scripts/b.html</u>

e agora:

**a.html**

``` html
<script type="text/javascript"> type="text/javascript">
window.open( 'b.html', '', 'width=300, height=200;')
</script>
```
ao acessarmos o arquivo <u>a.html</u>, o alert do nosso <u>b.html</u>, **que foi aberto como popup**, irá mostrar: **[Object Window]**

## <a href="http://wbruno.com.br/scripts/a.html" target="_blank">a.html</a>
