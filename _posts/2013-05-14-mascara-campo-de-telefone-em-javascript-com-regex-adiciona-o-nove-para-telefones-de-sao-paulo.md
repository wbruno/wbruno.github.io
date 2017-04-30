---
id: 2956
title: 'Mascara campo de telefone em javascript com regex &#8211; Adiciona o nove para telefones de são paulo'
date: 2013-05-14T17:10:03+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2956
permalink: /javascript-puro/mascara-campo-de-telefone-em-javascript-com-regex-adiciona-o-nove-para-telefones-de-sao-paulo/
dsq_thread_id:
  - "2115949496"
categories:
  - Javascript
tags:
  - máscara
---
Esse código abaixo, possui uma função que no evento onblur do campo, adiciona o dígito nove para telefones com ddd 11, caso o usuário tenha informado um telefone de dígito 11 e não tenha informado o nove.

Completo do post [Mascara campo de telefone em javascript com regex – Nono dígito – Telefones São Paulo](http://wbruno.com.br/2012/08/02/mascara-campo-de-telefone-em-javascript-com-regex-nono-digito-telefones-sao-paulo/)
  
<!--more-->

<pre class="javascript">&lt;html>
&lt;head>
    &lt;title>Mascara Telefone&lt;/title>
&lt;script type="text/javascript">
/* Máscaras ER */
function mascara(o, f) {
    v_obj = o;
    v_fun = f;
    setTimeout(execmascara, 1);
}
function execmascara() {
    v_obj.value = v_fun(v_obj.value)
}
function mtel(v) {
    v=v.replace(/\D/g,"");
    v=v.replace(/^(\d{2})(\d)/g,"($1) $2");
    v=v.replace(/(\d)(\d{4})$/,"$1-$2");
    return v;
}
function id(el) {
	return document.getElementById(el);
}
window.onload = function() {
	var $telefone = id('telefone');
	$telefone.onkeyup = function() {
		mascara( this, mtel );
	}
	$telefone.onblur = function() {
		var v = this.value;
		if( v.indexOf('(11)') !== -1 && v.length === 14) {
			this.value = v.replace(/\((\d{2})\) (\d{4})-(\d{4})/g,'($1) 9$2-$3');
		}
	}
}
&lt;/script>

&lt;/head>
&lt;body>

    &lt;input type="text" name="telefone" id="telefone" maxlength="15" />

&lt;/body>
&lt;/html>
</pre>