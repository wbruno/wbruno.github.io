---
id: 194
title: 'Rotina semelhante ao str_pad do php ao &#8216;sair do campo&#8217;'
date: 2011-03-12T00:12:46+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=194
permalink: /expressao-regular/rotina-semelhante-ao-str_pad-do-php-ao-sair-do-campo/
categories:
  - Expressão Regular
tags:
  - máscara
---
Referência do autor da base deste script:
  
<a href="http://elcio.com.br/ajax/mascara/" target="_blank">http://elcio.com.br/ajax/mascara/</a>

<pre name="code" class="javascript">&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
/* Máscaras ER */
function mascara(o,f){
        v_obj=o;
        v_fun=f;
        setTimeout("execmascara()",1);
}
function execmascara(){
        v_obj.value=v_fun(v_obj.value);
}
function id( el ){
        return document.getElementById( el );
}
function mnum(v){
    v=v.replace(/\D/g,"");//Remove tudo o que não é dígito
    return v;
}
window.onload = function()
{
        id('hash').onkeypress = function(){
                mascara( this, mnum );
        }
        id('hash').onblur = function(){
                var dig = this.value.length;

                while( dig&lt;3 ){
                        this.value = '0'+this.value;
                        dig++;
                }
        }
}
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
        &lt;form action="" method="post"&gt;
                &lt;input type="text" name="hash" id="hash" maxlength="3" /&gt;
        &lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>