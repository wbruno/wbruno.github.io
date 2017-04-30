---
id: 71
title: Copiar formulario, ao selecionar select
date: 2010-09-22T21:40:16+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=71
permalink: /javascript-puro/copiar-formulario-ao-selecionar-select/
categories:
  - Javascript
tags:
  - formulário
---
<pre name="code" class="html">&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
function id( el ){
        return document.getElementById( el );
}
function copia_apaga( copia, value ){
        return copia=='copia' ? value : '';
}
function copia_motorista( copia )
{
        id('nome_motorista').value = copia_apaga( copia, id('nome_proprietario').value );
        id('carteira_motorista').value = copia_apaga( copia, id('carteira_proprietario').value );
}
function selected( select_value, select )
{
        var options = select.getElementsByTagName('option');
        for( var i=0; i&lt;options.length; i++ )
        {
                if( options[i].value==select_value )
                        return options[i].selected = true;
        }
}
window.onload = function()
{
        id('vinculo').onchange = function()
        {
                if( this.value=='O Próprio' )
                {
                        copia_motorista( 'copia' );
                        selected( id('sexo_proprietario').value, id('sexo_motorista') );
                }
                else
                {
                        copia_motorista( 'apaga' );
                        selected( '', id('sexo_motorista') );
                }
        }
}
&lt;/script&gt;
&lt;style type="text/css"&gt;
label { display: block; }
&lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;
        &lt;form action="" method="post"&gt;
                                       
                &lt;fieldset&gt;
                        &lt;legend&gt;Proprietário&lt;/legend&gt;
                        &lt;label&gt;Nome: &lt;input type="text" name="nome_proprietario" id="nome_proprietario" value="Bruno" /&gt;&lt;/label&gt;
                        &lt;label&gt;Carteira: &lt;input type="text" name="carteira_proprietario" id="carteira_proprietario" value="14121988" /&gt;&lt;/label&gt;
                        &lt;label&gt;Sexo: &lt;select name="sexo_proprietario" id="sexo_proprietario"&gt;
                                &lt;option value=""&gt;--&lt;/option&gt;
                                &lt;option value="Feminino"&gt;Feminino&lt;/option&gt;
                                &lt;option value="Masculino" selected="selected"&gt;Masculino&lt;/option&gt;
                        &lt;/select&gt;&lt;/label&gt;
                &lt;/fieldset&gt;
               
                &lt;label&gt;Vínculo: &lt;select name="vinculo" id="vinculo"&gt;
                        &lt;option value=""&gt;--&lt;/option&gt;
                        &lt;option value="O Próprio"&gt;O Próprio&lt;/option&gt;
                        &lt;option value="Irmão"&gt;Irmão&lt;/option&gt;
                        &lt;option value="Desconhecido"&gt;Desconhecido&lt;/option&gt;
                &lt;/select&gt;&lt;/label&gt;
               
                &lt;fieldset&gt;
                        &lt;legend&gt;Motorista&lt;/legend&gt;
                        &lt;label&gt;Nome: &lt;input type="text" name="nome_motorista" id="nome_motorista" value="" /&gt;&lt;/label&gt;
                        &lt;label&gt;Carteira: &lt;input type="text" name="carteira_motorista" id="carteira_motorista" value="" /&gt;&lt;/label&gt;
                        &lt;label&gt;Sexo: &lt;select name="sexo_motorista" id="sexo_motorista"&gt;
                                &lt;option value=""&gt;--&lt;/option&gt;
                                &lt;option value="Feminino"&gt;Feminino&lt;/option&gt;
                                &lt;option value="Masculino"&gt;Masculino&lt;/option&gt;
                        &lt;/select&gt;&lt;/label&gt;
                &lt;/fieldset&gt;
        &lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>