---
id: 14
title: Demonstração função setInterval Javascript
date: 2009-08-26T20:08:40+00:00
author: wbruno
excerpt: Demostração de set interval
layout: post
guid: http://www.wbruno.com.br/blog/?p=14
permalink: /javascript-puro/demonstracao-funcao-setinterval-javascript/
categories:
  - Javascript
---
Dá uma olhada..

a cada 1 segundo e meio, vai aparecer um alert na tela.. e incrementar um contador&#8230;

``` html
<html>
<head>
<title>setInterval</title>
<script type="text/javascript">
        var i = ;
        window.onload = function()
        {
                window.setInterval(ver, 1500);
        }
        function ver()
        {
                i++;
                return alert('Chamou: '+i);
        }
</script>
</head>
<body>

</body>
</html>
```
