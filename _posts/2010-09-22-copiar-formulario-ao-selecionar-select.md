---
id: 71
title: Copiar formulario, ao selecionar select
date: 2010-09-22T21:40:16+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=71
permalink: /javascript-puro/copiar-formulario-ao-selecionar-select/
categories:
  - Javascript
tags:
  - formulário
---
``` html
<html>
<head>
<script type="text/javascript">
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
        for( var i=0; i<options.length; i++ )
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
</script>
<style type="text/css">
label { display: block; }
</style>
</head>
<body>
        <form action="" method="post">

                <fieldset>
                        <legend>Proprietário</legend>
                        <label>Nome: <input type="text" name="nome_proprietario" id="nome_proprietario" value="Bruno" /></label>
                        <label>Carteira: <input type="text" name="carteira_proprietario" id="carteira_proprietario" value="14121988" /></label>
                        <label>Sexo: <select name="sexo_proprietario" id="sexo_proprietario">
                                <option value="">--</option>
                                <option value="Feminino">Feminino</option>
                                <option value="Masculino" selected="selected">Masculino</option>
                        </select></label>
                </fieldset>

                <label>Vínculo: <select name="vinculo" id="vinculo">
                        <option value="">--</option>
                        <option value="O Próprio">O Próprio</option>
                        <option value="Irmão">Irmão</option>
                        <option value="Desconhecido">Desconhecido</option>
                </select></label>

                <fieldset>
                        <legend>Motorista</legend>
                        <label>Nome: <input type="text" name="nome_motorista" id="nome_motorista" value="" /></label>
                        <label>Carteira: <input type="text" name="carteira_motorista" id="carteira_motorista" value="" /></label>
                        <label>Sexo: <select name="sexo_motorista" id="sexo_motorista">
                                <option value="">--</option>
                                <option value="Feminino">Feminino</option>
                                <option value="Masculino">Masculino</option>
                        </select></label>
                </fieldset>
        </form>
</body>
</html>
```
