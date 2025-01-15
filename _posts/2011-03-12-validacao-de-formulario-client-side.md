---
id: 204
title: Validação de formulário client side
date: 2011-03-12T00:27:19+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=204
permalink: /javascript-puro/validacao-de-formulario-client-side/
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
function no_empty( campo ){
        if( campo.value=='' )
        {
                alert( "Preencha o campo '"+campo.title+"' !" );
                return 1;
        }
        else
                return 0;
}
window.onload = function(){
        id('f-teste').onsubmit = function()     {
                var erro = 0;
                erro += no_empty( id('marca') );
                erro += no_empty( id('idade') );

                if( erro ) return false;
        }
}
</script>
</head>
<body>
  <form action="enviando.asp" method="post" id="f-teste">
     <fieldset>
         <label><span>nome: </span>
         <input type="text" name="marca" id="marca" title="Nome da Marca" size="50"></label>

         <label><span>idade: </span>
         <input type="text" name="idade" id="idade" title="Idade" size="50"></label>

         <label><input type="submit" class="btn" value="Enviar" /></label>
         </fieldset>
  </form>
</body>
</html>
```

já postei <a href="http://forum.imasters.uol.com.br/index.php?/topic/408955-validar-campos-formulario/page__view__findpost__p__1606723" target="_blank">aqui</a> e <a href="http://forum.imasters.uol.com.br/index.php?/topic/411195-validacao/page__gopid__1616630&#038;#entry1616630" target="_blank">aqui</a> essa estrutura.
