---
id: 2939
title: Máscara javascript para peso com preenchimento ao contrário
date: 2013-04-11T10:36:31+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2939
permalink: /javascript-puro/mascara-javascript-para-peso-com-preenchimento-ao-contrario/
dsq_thread_id:
  - "2102408408"
categories:
  - Javascript
tags:
  - máscara
---
Fiz esse código pq nenhuma das minhas outras máscaras em javascript resolvia.

O comportamento é:
  
digitar: <var>1</var> aparecer <var>0,0001</var>
  
digitar: <var>12</var> aparecer <var>0,0012</var>
  
digitar: <var>123</var> aparecer <var>0,0123</var>
  
digitar: <var>1234</var> aparecer <var>0,1234</var>
  
digitar: <var>12345</var> aparecer <var>1,2345</var>
  
digitar: <var>123456</var> aparecer <var>12,3456</var>
  
digitar: <var>1234567</var> aparecer <var>123,4567</var>

O bloco do if pode ser refatorado para ficar mais &#8220;bonito&#8221; e menos manual. Mas já é uma idéia de como fazer essa máscara para &#8220;peso&#8221;, usando javascript e um pouquinho de expressão regular.

<pre class="javascript"><script type="text/javascript">
function id(el){
    return document.getElementById(el);
}
window.onload = function(){
  id('peso').onkeyup = function(){
    var v = this.value,
      integer = v.split(',')[0];


    v = v.replace(/\D/, "");
    v = v.replace(/^[0]+/, "");

    if(v.length <= 4 || !integer)
    {
      if(v.length === 1) v = '0,000' + v;
      if(v.length === 2) v = '0,00' + v;
      if(v.length === 3) v = '0,0' + v;
      if(v.length === 4) v = '0,' + v;
    } else {
      v = v.replace(/^(\d{1,})(\d{4})$/, "$1,$2");
    }

    this.value = v;
  }
};
</script>
<input type="text" name="peso" id="peso" maxlength="8" />

```