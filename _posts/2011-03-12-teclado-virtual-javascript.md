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
``` html
<html>
<head>
<script type="text/javascript">
function id( el ){
        return document.getElementById( el );
}
function val( destino, valor ){
        destino.value += valor;
}
var focus = false;
window.onload = function(){
       
       
        var botoes = id('teclado').getElementsByTagName('input');
        for( var i=0; i<botoes.length; i++ ){
                botoes[i].onclick = function(){
                        if( !focus ){ alert('coloque o foco em algum input');exit(); }

                        val( id( focus ), this.value );
                        id( focus ).focus();
                }
        }
       
        var inputs = id('area').getElementsByTagName('input');
        for( var i=0; i<inputs.length; i++ ){
                inputs[i].onfocus = function(){
                        focus = this.id;
                }
        }
        id('entrada_1').focus();
}
</script>
<style type="text/css">
* { margin: 0; padding: 0; border: 0; }
input { background: #fff; border: 1px solid #ccc; padding: 2px;}
#teclado { width: 400px; }
#teclado fieldset { width: 300px; text-align: center; float: left; margin: 2px; }
#teclado #numbers { float: right; width: 80px; }
fieldset { margin: 5px; }
</style>
</head>
<body>
        <form action="" method="post">
                <fieldset id="area">
                        <input type="text" name="entrada_1" id="entrada_1" /></label>
                        <input type="text" name="entrada_2" id="entrada_2" /></label>
                        <input type="text" name="entrada_3" id="entrada_3" /></label>
                </fieldset>
                <fieldset id="teclado">
                        <fieldset id="numbers">
                                <input type="button" name="7" value="7" />
                                <input type="button" name="8" value="8" />
                                <input type="button" name="9" value="9" />
                               
                                <input type="button" name="4" value="4" />
                                <input type="button" name="5" value="5" />
                                <input type="button" name="6" value="6" />
                               
                                <input type="button" name="1" value="1" />
                                <input type="button" name="2" value="2" />
                                <input type="button" name="3" value="3" />
                               
                                <input type="button" name="0" value="0" />
                        </fieldset>
                        <fieldset>
                                <input type="button" name="q" value="q" />
                                <input type="button" name="w" value="w" />
                                <input type="button" name="e" value="e" />
                                <input type="button" name="r" value="r" />
                                <input type="button" name="t" value="t" />
                                <input type="button" name="y" value="y" />
                                <input type="button" name="u" value="u" />
                                <input type="button" name="i" value="i" />
                                <input type="button" name="o" value="o" />
                                <input type="button" name="p" value="p" />
                        </fieldset>
                        <fieldset>
                                <input type="button" name="a" value="a" />
                                <input type="button" name="s" value="s" />
                                <input type="button" name="d" value="d" />
                                <input type="button" name="f" value="f" />
                                <input type="button" name="g" value="g" />
                                <input type="button" name="h" value="h" />
                                <input type="button" name="j" value="j" />
                                <input type="button" name="k" value="k" />
                                <input type="button" name="l" value="l" />
                                <input type="button" name="ç" value="ç" />
                        </fieldset>
                        <fieldset>                      
                                <input type="button" name="z" value="z" />
                                <input type="button" name="x" value="x" />
                                <input type="button" name="c" value="c" />
                                <input type="button" name="v" value="v" />                      
                                <input type="button" name="b" value="b" />
                                <input type="button" name="n" value="n" />
                                <input type="button" name="m" value="m" />
                        </fieldset>
                </fieldset>
        </form>
</body>
</html>
```