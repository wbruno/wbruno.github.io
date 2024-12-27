---
id: 2859
title: 'Formatar moeda no onblur &#8211; javascript sem jQuery'
date: 2012-11-23T07:00:03+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2859
permalink: /expressao-regular/formatar-moeda-no-onblur-javascript-sem-jquery/
dsq_thread_id:
  - "2100783080"
categories:
  - Expressão Regular
tags:
  - máscara
---
Diferente das demais máscaras de moeda em javascript, assim como essa minha que [formata usando Expressão Regular no onkeyUp do campo](https://wbruno.com.br/expressao-regular/diversas-mascaras-com-er/), a máscara que apresento agora, formata no evento onblur.

Aceita as entradas:

`,1 = 0,10<br />
,10 = 0,10<br />
1 = 1,00<br />
10 = 10,00<br />
100 = 100,00`

**money-blur.js**

``` js
'use strict';
function _signalFirst(v) {
  return /^(,|\.)/.test(v);
}
function _signalOne(v) {
  return /,|\.+\d$/.test(v);
}
function _onlyNumber(v) {
  return /^\d+$/.test(v);
}
function _rightPosition(v) {
  return /(,|\.)\d{2}$/.test(v);
}
function _format(v) {
  var length = v.length;

  if (_signalFirst(v)) {
    console.log('_signalFirst');

    v = v.replace(/[,.]/, '');
    if (length===2) v = '0,' + v + '0';
    else v = '0,' + v;
  } else if (_onlyNumber(v)) {
    console.log('_onlyNumber');

    v = v + ',00';
  } else if (_rightPosition(v)) {
    console.log('_rightPosition');

    v = v.replace(/[,.]/, '');
    v = v.replace(/(\d)(\d{2})$/, '$1,$2');
  } else if (_signalOne(v)) {
    console.log('_signalOne');

    v = v.replace(/[,.]/, '');
    v = v + '0';
    v = v.replace(/(\d)(\d{2})$/,"$1,$2");
  } else {
    v = v.replace(/[,.]/, '');
    v = v.replace(/(\d{1,3})$/g,"$1,00");
    v = v.replace(/(\d{1,3})(\d{3},00)$/,"$1.$2");
  }
  return v;
}

if (typeof exports !== 'undefined') {
  if (typeof module !== 'undefined' && module.exports) {
    exports = module.exports = _format;
  }
  exports._format = _format;
}

```

usando no teu html..

``` html
<script type="text/javascript"> type="text/javascript">
function id(el){
  return document.getElementById(el);
}
window.onload = function(){
  id('moeda').onkeyup = function() {
      var v = this.value;
      v = v.replace(/[^\d,.]/, '');
      this.value = v;
  };
  id('moeda').onblur = function() {
    var v = this.value;
    this.value = _format(v);
  }
};
</script>
<input type="text" name="moeda" id="moeda" />

```

É isso galera. Comente caso usem =)

## Demonstração no Github

<http://wbruno.github.io/examples/money-blur/>
