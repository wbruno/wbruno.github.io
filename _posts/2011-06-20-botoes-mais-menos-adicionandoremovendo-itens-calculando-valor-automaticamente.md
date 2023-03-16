---
id: 1105
title: Botões Mais e Menos, adicionando/removendo itens, e calculando valor automaticamente
date: 2011-06-20T22:03:51+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1105
permalink: /javascript-puro/botoes-mais-menos-adicionandoremovendo-itens-calculando-valor-automaticamente/
dsq_thread_id:
  - "2106282793"
categories:
  - Javascript
tags:
  - cálculo
---
Bom.. bem simples e básico..

porém fica de exemplo, para quem precisar.
  
<!--more-->

``` html
<html>
<head>
<script type="text/javascript">
function id( el ){
        return document.getElementById( el );
}
window.onload = function(){
        id('mais').onclick = function(){
                id('format').value = parseInt( id('format').value )+1;
                
                id('total').value = 20*id('format').value;
        }
        id('menos').onclick = function(){
                if( id('format').value>0 )
                        id('format').value = parseInt( id('format').value )-1;
                
                id('total').value = 20*id('format').value;
        }
}       
</script>
</head>
<body>
        <input type="button" name="mais" id="mais" value="+" />
        <input type="button" name="menos" id="menos" value="-" />
        
        <br />
        Formatacao <input type="text" name="format" value="0" id="format" size="2" /> x 20,00
        
        <br /><br />
        Total: <input type="text" name="total" id="total" value="" />
</body>
</html>
```

É isso ai, só mais um script rápido que criei para responder uma dúvida no fórum.