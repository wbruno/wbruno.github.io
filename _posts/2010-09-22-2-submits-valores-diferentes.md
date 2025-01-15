---
id: 73
title: 2 submits valores diferentes
date: 2010-09-22T21:41:09+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=73
permalink: /javascript-puro/2-submits-valores-diferentes/
categories:
  - Javascript
---
``` php
<?php
        if( $_SERVER['REQUEST_METHOD']=='POST' )
        {
                echo '<pre>';
                var_dump( $_POST );
                echo '</pre><br />';

                if( $_POST['action']=='editar' )
                        echo 'Edite!!';
                else
                        echo 'Excluaaa!!';
        }
?>
<html>
<head>
<script type="text/javascript">
window.onload = function()
{
        id('editar').onclick = function( e )
        {
                enviar( e, 'editar' );
        }
        id('excluir').onclick = function( e )
        {
                enviar( e, 'excluir' );
        }
}
function enviar( event, action )
{
        disablelink( event );
        id('action').value = action;
        id('f-teste').submit();
}
function id( el ){
        return document.getElementById( el );
}
/* http://www.javascriptkit.com/jsref/event.shtml */
function disablelink( e ){
        var evt = window.event || e
        if (evt.preventDefault) //supports preventDefault?
                evt.preventDefault()
        else //IE browser
                return false
}
</script>
</head>
<body>
        <form method="post" action="" id="f-teste">
                <input type="hidden" name="action" id="action" value="" />
                <input type="text" name="texto" />
                <input type="text" name="idade" />
                <a href="#" id="editar">Editar</a>
                <a href="#" id="excluir">Excluir</a>
        </form>
</body>
</html>
```

Sem javascript, apenas com HTML puro:

``` php
<?php
if( $_SERVER['REQUEST_METHOD']=='POST' )
{
  echo '<pre>';
  var_dump( $_POST );
  echo '</pre><br />';

  if( $_POST['action']=='editar' )
    echo 'Edite!!';
  else
    echo 'Excluaaa!!';
}
?>
<html>
<head>
  <script type="text/javascript">

  </script>
</head>
<body>
  <form method="post" action="" id="f-teste">
    <input type="hidden" name="action" id="action" value="" />
    <input type="text" name="texto" />
    <input type="text" name="idade" />

    <input type="submit" name="action" value="editar" />
    <input type="submit" name="action" value="excluir" />
  </form>
</body>
</html>
```
