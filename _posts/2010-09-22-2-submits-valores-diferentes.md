---
id: 73
title: 2 submits valores diferentes
date: 2010-09-22T21:41:09+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=73
permalink: /javascript-puro/2-submits-valores-diferentes/
categories:
  - Javascript
---
<pre name="code" class="php">&lt;?php
        if( $_SERVER['REQUEST_METHOD']=='POST' )
        {
                echo '&lt;pre&gt;';
                var_dump( $_POST );
                echo '&lt;/pre&gt;&lt;br /&gt;';

                if( $_POST['action']=='editar' )
                        echo 'Edite!!';
                else
                        echo 'Excluaaa!!';
        }
?&gt;
&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
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
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
        &lt;form method="post" action="" id="f-teste"&gt;
                &lt;input type="hidden" name="action" id="action" value="" /&gt;
                &lt;input type="text" name="texto" /&gt;
                &lt;input type="text" name="idade" /&gt;
                &lt;a href="#" id="editar"&gt;Editar&lt;/a&gt;
                &lt;a href="#" id="excluir"&gt;Excluir&lt;/a&gt;
        &lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

Sem javascript, apenas com HTML puro:

<pre name="code" class="html">&lt;?php
if( $_SERVER['REQUEST_METHOD']=='POST' )
{
	echo '&lt;pre&gt;';
	var_dump( $_POST );
	echo '&lt;/pre&gt;&lt;br /&gt;';

	if( $_POST['action']=='editar' )
		echo 'Edite!!';
	else
		echo 'Excluaaa!!';
}
?&gt;
&lt;html&gt;
&lt;head&gt;
	&lt;script type="text/javascript"&gt;

	&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
	&lt;form method="post" action="" id="f-teste"&gt;
		&lt;input type="hidden" name="action" id="action" value="" /&gt;
		&lt;input type="text" name="texto" /&gt;
		&lt;input type="text" name="idade" /&gt;

		&lt;input type="submit" name="action" value="editar" /&gt;
		&lt;input type="submit" name="action" value="excluir" /&gt;
	&lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>