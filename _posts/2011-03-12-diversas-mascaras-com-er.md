---
id: 196
title: Diversas máscaras com ER
date: 2011-03-12T00:20:32+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=196
permalink: /expressao-regular/diversas-mascaras-com-er/
dsq_thread_id:
  - "2101290960"
categories:
  - Expressão Regular
tags:
  - máscara
---
A referência do criador desse script está aqui:

<a href="http://elcio.com.br/ajax/mascara/" target="_blank">http://elcio.com.br/ajax/mascara/</a>

de minha autoria, é a máscara mvalor, e mais algumas simples como a mrg

``` js
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
    v=v.replace(/\D/g,"")                    //Remove tudo o que não é dígito
    v=v.replace(/^(\d{5})(\d)/,"$1-$2")         //Esse é tão fácil que não merece explicações
    return v
}
function mtel(v){
    v=v.replace(/\D/g,"");             //Remove tudo o que não é dígito
    v=v.replace(/^(\d{2})(\d)/g,"($1) $2"); //Coloca parênteses em volta dos dois primeiros dígitos
    v=v.replace(/(\d)(\d{4})$/,"$1-$2");    //Coloca hífen entre o quarto e o quinto dígitos
    return v;
}
function cnpj(v){
    v=v.replace(/\D/g,"")                           //Remove tudo o que não é dígito
    v=v.replace(/^(\d{2})(\d)/,"$1.$2")             //Coloca ponto entre o segundo e o terceiro dígitos
    v=v.replace(/^(\d{2})\.(\d{3})(\d)/,"$1.$2.$3") //Coloca ponto entre o quinto e o sexto dígitos
    v=v.replace(/\.(\d{3})(\d)/,".$1/$2")           //Coloca uma barra entre o oitavo e o nono dígitos
    v=v.replace(/(\d{4})(\d)/,"$1-$2")              //Coloca um hífen depois do bloco de quatro dígitos
    return v
}
function mcpf(v){
    v=v.replace(/\D/g,"")                    //Remove tudo o que não é dígito
    v=v.replace(/(\d{3})(\d)/,"$1.$2")       //Coloca um ponto entre o terceiro e o quarto dígitos
    v=v.replace(/(\d{3})(\d)/,"$1.$2")       //Coloca um ponto entre o terceiro e o quarto dígitos
                                             //de novo (para o segundo bloco de números)
    v=v.replace(/(\d{3})(\d{1,2})$/,"$1-$2") //Coloca um hífen entre o terceiro e o quarto dígitos
    return v
}
function mdata(v){
    v=v.replace(/\D/g,"");                    //Remove tudo o que não é dígito
    v=v.replace(/(\d{2})(\d)/,"$1/$2");
    v=v.replace(/(\d{2})(\d)/,"$1/$2");

    v=v.replace(/(\d{2})(\d{2})$/,"$1$2");
    return v;
}
function mtempo(v){
    v=v.replace(/\D/g,"");                    //Remove tudo o que não é dígito
    v=v.replace(/(\d{1})(\d{2})(\d{2})/,"$1:$2.$3");
    return v;
}
function mhora(v){
    v=v.replace(/\D/g,"");                    //Remove tudo o que não é dígito
    v=v.replace(/(\d{2})(\d)/,"$1h$2");
    return v;
}
function mrg(v){
    v=v.replace(/\D/g,"");                                      //Remove tudo o que não é dígito
        v=v.replace(/(\d)(\d{7})$/,"$1.$2");    //Coloca o . antes dos últimos 3 dígitos, e antes do verificador
        v=v.replace(/(\d)(\d{4})$/,"$1.$2");    //Coloca o . antes dos últimos 3 dígitos, e antes do verificador
        v=v.replace(/(\d)(\d)$/,"$1-$2");               //Coloca o - antes do último dígito
    return v;
}
function mnum(v){
    v=v.replace(/\D/g,"");                                      //Remove tudo o que não é dígito
    return v;
}
function mvalor(v){
    v=v.replace(/\D/g,"");//Remove tudo o que não é dígito
    v=v.replace(/(\d)(\d{8})$/,"$1.$2");//coloca o ponto dos milhões
    v=v.replace(/(\d)(\d{5})$/,"$1.$2");//coloca o ponto dos milhares

    v=v.replace(/(\d)(\d{2})$/,"$1,$2");//coloca a virgula antes dos 2 últimos dígitos
    return v;
}
```

## Forma de uso

``` html
<input type="text" onkeyup="mascara(this, mvalor);" />
```

Se você está precisando de uma máscara para telefone com o nono dígito, veja aqui: [mascara com expressão regular do nono dígito do estado de são paulo](https://wbruno.com.br/expressao-regular/mascara-campo-de-telefone-em-javascript-com-regex-nono-digito-telefones-sao-paulo/).
