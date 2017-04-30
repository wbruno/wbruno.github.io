---
id: 42
title: Mascaras com jQuery e JS, trocando de campo no maxLength
date: 2010-05-06T21:47:17+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=42
permalink: /expressao-regular/mascaras-com-jquery-e-js-trocando-de-campo-no-maxlength/
dsq_thread_id:
  - "2100987728"
categories:
  - Expressão Regular
tags:
  - máscara
---
Se você tiver disposto à trocar de máscara, essas com ER são muito boas, e não te darão esse tipo de problema:
  
<a title="Link externo" rel="nofollow external" href="http://forum.imasters.uol.com.br/index.php?/topic/392937-evitar-letras-no-lugar-de-digitos/page__view__findpost__p__1532871">http://forum.imaster&#8230;ost__p__1532871</a>

Referência do autor da base deste script:
  
<a href="http://elcio.com.br/ajax/mascara/" target="_blank">http://elcio.com.br/ajax/mascara/</a>

<pre name="code" class="javascript">&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
/* Máscaras ER */
function mascara(o,f){
    v_obj=o
    v_fun=f
    setTimeout("execmascara()",1)
}
function execmascara(){
    v_obj.value=v_fun(v_obj.value)
}
function mcep(v){
    v=v.replace(/\D/g,"")                    //Remove tudo o que não é dígito
    v=v.replace(/^(\d{5})(\d)/,"$1-$2")         //Esse é tão fácil que não merece explicações
    return v
}
function mdata(v){
    v=v.replace(/\D/g,"");                    //Remove tudo o que não é dígito
    v=v.replace(/(\d{2})(\d)/,"$1/$2");      
    v=v.replace(/(\d{2})(\d)/,"$1/$2");      

    v=v.replace(/(\d{2})(\d{2})$/,"$1$2");
    return v;
}
function mrg(v){
        v=v.replace(/\D/g,'');
        v=v.replace(/^(\d{2})(\d)/g,"$1.$2");
        v=v.replace(/(\d{3})(\d)/g,"$1.$2");
        v=v.replace(/(\d{3})(\d)/g,"$1-$2");
        return v;
}
function mvalor(v){
    v=v.replace(/\D/g,"");//Remove tudo o que não é dígito
    v=v.replace(/(\d)(\d{8})$/,"$1.$2");//coloca o ponto dos milhões
    v=v.replace(/(\d)(\d{5})$/,"$1.$2");//coloca o ponto dos milhares

    v=v.replace(/(\d)(\d{2})$/,"$1,$2");//coloca a virgula antes dos 2 últimos dígitos
    return v;
}
function id( el ){
        return document.getElementById( el );
}
function next( el, next )
{
        if( el.value.length &gt;= el.maxLength )
                id( next ).focus();
}
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
        Real: &lt;input type="text" name="valor" onkeypress="mascara( this, mvalor ); next( this, 'cep' );" maxlength="14" /&gt;
        &lt;br /&gt;
        CEP: &lt;input type="text" name="cep" id="cep" onkeypress="mascara(this, mcep); next( this, 'rg' );" size="10" maxlength="9" value="" /&gt;
        &lt;br /&gt;
        RG: &lt;input type="text" name="rg" id="rg" onkeypress="mascara(this, mrg); next( this, 'data' );" size="14" maxlength="12" value="" /&gt;
        &lt;br /&gt;
        Data: &lt;input type="text" name="data" id="data" onkeypress="mascara(this, mdata);" size="14" maxlength="10" value="" /&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>

Mas qnto ao que você pediu, é possível fazer com ER, e assim continuar usando a máscara jQuery. Porém dá um pouquinho de trabalho.. veja:

<pre name="code" class="javascript">&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript" src="jquery.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="jquery.maskedinput.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript"&gt;
$(document).ready(function(){
        var cep = $("input[name='cep']");
        var rg = $("input[name='rg']");
        var data = $("input[name='data']");

        $( cep ).mask('99999-999');
        $( rg ).mask('99.999.999-9');
        $( data ).mask('99/99/9999');

        $("input[name='cep']").keyup(function(){
                next( $(this), rg );
        });
        $("input[name='rg']").keyup(function(){
                next( $(this), data );
        });
});
function next( el, next )
{
        var val = $( el ).val();
        var filtrado = val.replace(/[^a-zA-Z0-9]/g, '');
        // ER para remover tudo oque não for nem letra e nem número    
        var mask = val.match(/[-.]/g);
        // ER para saber quantos caracteres da máscara fazem parte da string final

        if( filtrado.length == $( el ).attr('maxLength')-mask.length )
                $( next ).focus();
}
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
        CEP: &lt;input type="text" name="cep" size="10" maxlength="9" value="" /&gt;
        &lt;br /&gt;
        RG: &lt;input type="text" name="rg" size="14" maxlength="12" value="" /&gt;
        &lt;br /&gt;
        Data: &lt;input type="text" name="data" size="14" maxlength="10" value="" /&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>