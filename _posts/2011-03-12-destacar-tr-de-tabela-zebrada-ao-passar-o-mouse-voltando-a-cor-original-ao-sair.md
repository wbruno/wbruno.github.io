---
id: 214
title: Destacar Tr De Tabela Zebrada, Ao Passar O Mouse. Voltando A Cor Original Ao Sair
date: 2011-03-12T00:35:08+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=214
permalink: /javascript-puro/destacar-tr-de-tabela-zebrada-ao-passar-o-mouse-voltando-a-cor-original-ao-sair/
dsq_thread_id:
  - "2103188508"
categories:
  - Javascript
---
``` html
<html>
<head>
<script type="text/javascript">
function id( el ){
        return document.getElementById( el );
}
var cor_antiga;
window.onload = function()
{
        var trs = id('lista').getElementsByTagName('tr');
        for( var i=0; i<trs.length; i++ )
        {
                trs[i].onmouseover = function()
                {
                        cor_antiga = this.style.backgroundColor;
                        this.style.backgroundColor = '#ff0';
                }
                trs[i].onmouseout = function()
                {
                        this.style.backgroundColor = cor_antiga;
                }
        }
}

</script>
<style type="text/css">
.dif {
        background: #ccc;
}
</style>
</head>
<body>
        <table id="lista">
                <thead>
                        <tr>
                                <th>ID</th>
                                <th>Nome</th>
                                <th>Editar</th>
                                <th>Excluir</th>
                        </tr>
                </thead>
                <tbody>
                        <tr class="dif">
                                <td>1</td>
                                <td>Bruno</td>
                                <td>edit</td>
                                <td>del</td>
                        </tr>
                        <tr>
                                <td>7</td>
                                <td>Rocha</td>
                                <td>edit</td>
                                <td>del</td>
                        </tr>
                        <tr class="dif">
                                <td>15</td>
                                <td>Moraes</td>
                                <td>edit</td>
                                <td>del</td>
                        </tr>
                </tbody>
        </table>
</body>
</html>
```
