---
id: 212
title: Teclado Virtual Javascript
date: 2011-03-12T00:34:17+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=212
permalink: /javascript-puro/teclado-virtual-javascript/
dsq_thread_id:
  - "2103596984"
categories:
  - Javascript
---
<pre name="code" class="html">&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
function id( el ){
        return document.getElementById( el );
}
function val( destino, valor ){
        destino.value += valor;
}
var focus = false;
window.onload = function(){
       
       
        var botoes = id('teclado').getElementsByTagName('input');
        for( var i=0; i&lt;botoes.length; i++ ){
                botoes[i].onclick = function(){
                        if( !focus ){ alert('coloque o foco em algum input');exit(); }

                        val( id( focus ), this.value );
                        id( focus ).focus();
                }
        }
       
        var inputs = id('area').getElementsByTagName('input');
        for( var i=0; i&lt;inputs.length; i++ ){
                inputs[i].onfocus = function(){
                        focus = this.id;
                }
        }
        id('entrada_1').focus();
}
&lt;/script&gt;
&lt;style type="text/css"&gt;
* { margin: 0; padding: 0; border: 0; }
input { background: #fff; border: 1px solid #ccc; padding: 2px;}
#teclado { width: 400px; }
#teclado fieldset { width: 300px; text-align: center; float: left; margin: 2px; }
#teclado #numbers { float: right; width: 80px; }
fieldset { margin: 5px; }
&lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;
        &lt;form action="" method="post"&gt;
                &lt;fieldset id="area"&gt;
                        &lt;input type="text" name="entrada_1" id="entrada_1" /&gt;&lt;/label&gt;
                        &lt;input type="text" name="entrada_2" id="entrada_2" /&gt;&lt;/label&gt;
                        &lt;input type="text" name="entrada_3" id="entrada_3" /&gt;&lt;/label&gt;
                &lt;/fieldset&gt;
                &lt;fieldset id="teclado"&gt;
                        &lt;fieldset id="numbers"&gt;
                                &lt;input type="button" name="7" value="7" /&gt;
                                &lt;input type="button" name="8" value="8" /&gt;
                                &lt;input type="button" name="9" value="9" /&gt;
                               
                                &lt;input type="button" name="4" value="4" /&gt;
                                &lt;input type="button" name="5" value="5" /&gt;
                                &lt;input type="button" name="6" value="6" /&gt;
                               
                                &lt;input type="button" name="1" value="1" /&gt;
                                &lt;input type="button" name="2" value="2" /&gt;
                                &lt;input type="button" name="3" value="3" /&gt;
                               
                                &lt;input type="button" name="0" value="0" /&gt;
                        &lt;/fieldset&gt;
                        &lt;fieldset&gt;
                                &lt;input type="button" name="q" value="q" /&gt;
                                &lt;input type="button" name="w" value="w" /&gt;
                                &lt;input type="button" name="e" value="e" /&gt;
                                &lt;input type="button" name="r" value="r" /&gt;
                                &lt;input type="button" name="t" value="t" /&gt;
                                &lt;input type="button" name="y" value="y" /&gt;
                                &lt;input type="button" name="u" value="u" /&gt;
                                &lt;input type="button" name="i" value="i" /&gt;
                                &lt;input type="button" name="o" value="o" /&gt;
                                &lt;input type="button" name="p" value="p" /&gt;
                        &lt;/fieldset&gt;
                        &lt;fieldset&gt;
                                &lt;input type="button" name="a" value="a" /&gt;
                                &lt;input type="button" name="s" value="s" /&gt;
                                &lt;input type="button" name="d" value="d" /&gt;
                                &lt;input type="button" name="f" value="f" /&gt;
                                &lt;input type="button" name="g" value="g" /&gt;
                                &lt;input type="button" name="h" value="h" /&gt;
                                &lt;input type="button" name="j" value="j" /&gt;
                                &lt;input type="button" name="k" value="k" /&gt;
                                &lt;input type="button" name="l" value="l" /&gt;
                                &lt;input type="button" name="ç" value="ç" /&gt;
                        &lt;/fieldset&gt;
                        &lt;fieldset&gt;                      
                                &lt;input type="button" name="z" value="z" /&gt;
                                &lt;input type="button" name="x" value="x" /&gt;
                                &lt;input type="button" name="c" value="c" /&gt;
                                &lt;input type="button" name="v" value="v" /&gt;                      
                                &lt;input type="button" name="b" value="b" /&gt;
                                &lt;input type="button" name="n" value="n" /&gt;
                                &lt;input type="button" name="m" value="m" /&gt;
                        &lt;/fieldset&gt;
                &lt;/fieldset&gt;
        &lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>