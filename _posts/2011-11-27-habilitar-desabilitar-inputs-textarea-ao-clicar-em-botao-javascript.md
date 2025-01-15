---
id: 1630
title: 'Habilitar e Desabilitar inputs e textarea ao clicar em botão - JavaScript'
date: 2011-11-27T17:09:51+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1630
permalink: /javascript-puro/habilitar-desabilitar-inputs-textarea-ao-clicar-em-botao-javascript/
dsq_thread_id:
  - "2102530361"
categories:
  - Javascript
---
Um botão habilita e outro desabilita, setando .disabled = true;

<!--more-->

``` html
<html>
<head>
<script type="text/javascript">
function toogle_disabled( bool )
{
  var input = document.getElementsByTagName('input');
  var textarea = document.getElementsByTagName('textarea');

  for( var i=0; i<=(input.length-1); i++ )
  {
    if( input[i].type!='button' )
      input[i].disabled = bool;
  }
  for( var i=0; i<=(textarea.length-1); i++ )
  {
    textareat[i].disabled = bool;
  }
}
</script>
</head>
<body>
  <form>
    <input type="button" onclick="toogle_disabled( false )" value="Habilitar" />
    <input type="button" onclick="toogle_disabled( true )" value="Desabilitar" />

    <br /><br />
    Nome: <input type="text" name="nome" />
    Local: <input type="text" name="local" />
    <br>
    Nome: <input type="text" name="nome2" />
    Local: <input type="text" name="local2" />

  </form>
</body>
</html>
```
