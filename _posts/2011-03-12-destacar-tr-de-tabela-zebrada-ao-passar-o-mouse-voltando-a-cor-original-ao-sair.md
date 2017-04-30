---
id: 214
title: Destacar Tr De Tabela Zebrada, Ao Passar O Mouse. Voltando A Cor Original Ao Sair
date: 2011-03-12T00:35:08+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=214
permalink: /javascript-puro/destacar-tr-de-tabela-zebrada-ao-passar-o-mouse-voltando-a-cor-original-ao-sair/
dsq_thread_id:
  - "2103188508"
categories:
  - Javascript
---
<pre name="code" class="html">&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
function id( el ){
        return document.getElementById( el );
}
var cor_antiga;
window.onload = function()
{
        var trs = id('lista').getElementsByTagName('tr');
        for( var i=0; i&lt;trs.length; i++ )
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

&lt;/script&gt;
&lt;style type="text/css"&gt;
.dif {
        background: #ccc;
}
&lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;
        &lt;table id="lista"&gt;
                &lt;thead&gt;
                        &lt;tr&gt;
                                &lt;th&gt;ID&lt;/th&gt;
                                &lt;th&gt;Nome&lt;/th&gt;
                                &lt;th&gt;Editar&lt;/th&gt;
                                &lt;th&gt;Excluir&lt;/th&gt;
                        &lt;/tr&gt;
                &lt;/thead&gt;
                &lt;tbody&gt;
                        &lt;tr class="dif"&gt;
                                &lt;td&gt;1&lt;/td&gt;
                                &lt;td&gt;Bruno&lt;/td&gt;
                                &lt;td&gt;edit&lt;/td&gt;
                                &lt;td&gt;del&lt;/td&gt;
                        &lt;/tr&gt;
                        &lt;tr&gt;
                                &lt;td&gt;7&lt;/td&gt;
                                &lt;td&gt;Rocha&lt;/td&gt;
                                &lt;td&gt;edit&lt;/td&gt;
                                &lt;td&gt;del&lt;/td&gt;
                        &lt;/tr&gt;
                        &lt;tr class="dif"&gt;
                                &lt;td&gt;15&lt;/td&gt;
                                &lt;td&gt;Moraes&lt;/td&gt;
                                &lt;td&gt;edit&lt;/td&gt;
                                &lt;td&gt;del&lt;/td&gt;
                        &lt;/tr&gt;
                &lt;/tbody&gt;
        &lt;/table&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>