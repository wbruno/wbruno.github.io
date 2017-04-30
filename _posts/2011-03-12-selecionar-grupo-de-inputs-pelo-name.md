---
id: 210
title: Selecionar grupo de inputs pelo name
date: 2011-03-12T00:33:32+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=210
permalink: /javascript-puro/selecionar-grupo-de-inputs-pelo-name/
categories:
  - Javascript
---
<pre name="code" class="javascript">&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
function id( el ){
        return document.getElementById( el );
}
window.onload = function()
{
        var inputs = id('f-teste').getElementsByTagName('input');
        var result = '';
        for( var i=0; i&lt;inputs.length; i++ )
        {
                if( inputs[i].name=='id_cod[]' )
                        result += 'name: '+inputs[i].name+' value: '+inputs[i].value+'&lt;br /&gt;';
        }
        id('result').innerHTML = result;
}
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
        &lt;form action="" method="post" id="f-teste"&gt;
                &lt;input type="hidden" name="id_cod[]" value="1" /&gt;
               
                &lt;input type="text" name="produto[]" value="Um" /&gt;
               
                &lt;input type="hidden" name="id_cod[]" value="5" /&gt;
                &lt;input type="text" name="produto[]" value="Dois" /&gt;
                &lt;input type="hidden" name="id_cod[]" value="15" /&gt;
                &lt;input type="hidden" name="id_cod[]" value="7" /&gt;
               
                &lt;input type="submit" name="ok" value="ok" /&gt;
        &lt;/form&gt;
        &lt;div id="result"&gt;&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>