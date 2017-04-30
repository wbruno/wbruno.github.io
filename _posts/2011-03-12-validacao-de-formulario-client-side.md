---
id: 204
title: Validação de formulário client side
date: 2011-03-12T00:27:19+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=204
permalink: /javascript-puro/validacao-de-formulario-client-side/
categories:
  - Javascript
---
<pre name="code" class="html">&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
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
        id('f-teste').onsubmit = function()     {
                var erro = 0;
                erro += no_empty( id('marca') );
                erro += no_empty( id('idade') );

                if( erro ) return false;
        }
}
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;form action="enviando.asp" method="post" id="f-teste"&gt;
     &lt;fieldset&gt;
         &lt;label&gt;&lt;span&gt;nome: &lt;/span&gt;
         &lt;input type="text" name="marca" id="marca" title="Nome da Marca" size="50"&gt;&lt;/label&gt;

         &lt;label&gt;&lt;span&gt;idade: &lt;/span&gt;
         &lt;input type="text" name="idade" id="idade" title="Idade" size="50"&gt;&lt;/label&gt;

         &lt;label&gt;&lt;input type="submit" class="btn" value="Enviar" /&gt;&lt;/label&gt;
         &lt;/fieldset&gt;
  &lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>

já postei <a href="http://forum.imasters.uol.com.br/index.php?/topic/408955-validar-campos-formulario/page__view__findpost__p__1606723" target="_blank">aqui</a> e <a href="http://forum.imasters.uol.com.br/index.php?/topic/411195-validacao/page__gopid__1616630&#038;#entry1616630" target="_blank">aqui</a> essa estrutura.