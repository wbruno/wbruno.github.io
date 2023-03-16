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
``` html
<html>
<head>
<script type="text/javascript">
function id( el ){
        return document.getElementById( el );
}
window.onload = function()
{
        var inputs = id('f-teste').getElementsByTagName('input');
        var result = '';
        for( var i=0; i<inputs.length; i++ )
        {
                if( inputs[i].name=='id_cod[]' )
                        result += 'name: '+inputs[i].name+' value: '+inputs[i].value+'<br />';
        }
        id('result').innerHTML = result;
}
</script>
</head>
<body>
        <form action="" method="post" id="f-teste">
                <input type="hidden" name="id_cod[]" value="1" />
               
                <input type="text" name="produto[]" value="Um" />
               
                <input type="hidden" name="id_cod[]" value="5" />
                <input type="text" name="produto[]" value="Dois" />
                <input type="hidden" name="id_cod[]" value="15" />
                <input type="hidden" name="id_cod[]" value="7" />
               
                <input type="submit" name="ok" value="ok" />
        </form>
        <div id="result"></div>
</body>
</html>
```