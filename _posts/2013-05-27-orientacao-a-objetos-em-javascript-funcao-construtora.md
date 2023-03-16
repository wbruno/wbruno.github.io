---
id: 2993
title: 'Orientação a Objetos em Javascript &#8211; Função Construtora'
date: 2013-05-27T07:00:35+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2993
permalink: /javascript-puro/orientacao-a-objetos-em-javascript-funcao-construtora/
dsq_thread_id:
  - "2100742109"
categories:
  - Javascript
tags:
  - oo
---
Javascript é uma linguagem muito flexível.

[<img class="aligncenter size-full wp-image-2978" alt="js-logo" src="/wp-content/uploads/2013/05/js-logo.jpg" width="800" height="341" srcset="/wp-content/uploads/2013/05/js-logo.jpg 800w, /wp-content/uploads/2013/05/js-logo-300x127.jpg 300w" sizes="(max-width: 800px) 100vw, 800px" />](/wp-content/uploads/2013/05/js-logo.jpg)

E apesar de muitos desenvolvedores não terem conhecimento, javascript é muito orientada a objetos. Tanto que só existem 5 tipos primitivos que não são objetos na linguagem: numérico, string, booleano, null e undefined. Sendo que os 3 primeiros ainda podem ser convertidos em objetos pela própria linguagem internamente, ou por nós mesmos.

Eu já mostrei como é a [Orientação a Objetos em Javascript, usando objetos literais](http://wbruno.com.br/javascript-puro/afinal-como-e-orientacao-a-objetos-em-javascript-exemplos/). Particularmente, esse é estilo que eu prefiro. Mas nem por isso é o único correto. Existem outras formas de se programar com os conceitos de objetos em javascript.

<!--more-->

## Sem Classes

Vale a pena repetir: javascript não possui classes. E não possui por que não precisa, tanto que a ECMA4 foi abandonada por isso. Ao pensar em javascript, pense diretamente em objetos (afinal, quase tudo já o é).

## Funções Construtoras

Você pode criar objetos usando funções construtoras:

<pre class="javascript">var tt = new Tooltip();
tt.init();
```

Uma maneira de chegar a este código em javascript, é definindo a nossa função construtora:

<pre class="javascript">function Tooltip() {
    this.init = function() {
        //..
    }
}
```

O problema disso, é que sempre que instanciarmos um novo objeto, a função init será novamente criada na memória, e nem sempre isso é bom ao nosso projeto.

<pre class="javascript">var tt = new Tooltip();//aloca o objeto tt, criando a função init
var tt2 = new Tooltip();//aloca o objeto tt2, criando novamente init para este objeto agora```

## .prototype

Se adicionarmos o método init ao prototipo do objeto, todos as instâncias herdarão esse método e não estaremos enchendo a memória com declarações repetidas.

<pre class="javascript">function Tooltip() {}
Tooltip.prototype.init = function() {}
```

No github: <a href="https://github.com/wbruno/examples/tree/gh-pages/tt" rel="external">https://github.com/wbruno/examples/tree/gh-pages/tt</a> eu coloquei algumas formas diferentes de programar javascript.

Esse tooltip funciona basicamente só com css, através do pseudo seletor <var>:hover</var>. O papel do javascript, é procurar o conteúdo do tooltip apartir do atributo data-rel, e reescrever a marcação html do elemento que disparou o tooltip.

<pre class="javascript">var Tooltip =(function(){
  "use strict";

  function Tooltip() {}
  Tooltip.prototype.init = function(objs) {
    var i = objs.length;
    while(i--) {
      var obj = objs[i],
        wrap = this.createWrap(obj),
        ttContent = this.getContent(obj);

      wrap.appendChild(ttContent);
    }
    return objs;
  };
  Tooltip.prototype.createWrap = function(obj) {
    var wrap = document.createElement('span');
    wrap.className = 'tt-wrap';
    obj.parentNode.replaceChild(wrap, obj);
    wrap.appendChild(obj);
    return wrap;
  };
  Tooltip.prototype.getContent = function(obj) {
    var rel = obj.getAttribute('data-rel');
    return document.querySelector(rel);
  };
  return Tooltip;
}());

var $ = function(selector) {
  return document.querySelectorAll(selector);
};
window.addEventListener("load", function() {
  var tt = new Tooltip();
  tt.init($('.tt'));
  tt.init($('#another'));
});
```

## Visibilidade

Também usei o pattern de revelação nesta versão do código, mas diferente do código com objeto literal, onde apenas a função tt.init(), estava acessível ao mundo externo, aqui, todo o objeto Tooltip é público, através das suas instâncias.

<pre class="javascript">for(var prop in tt) {
    console.log(prop);//init, createWrap, getContent
  }
  console.log(tt.init);//function()
  console.log(tt.createWrap);//function()
  console.log(tt.getContent);//function()
```

## Instâncias

Quando adicionamos um método ao prototype de um objeto todas as instâncias herdarão esse método. Mas o objeto em si não. Veja a saída:

<pre class="javascript">console.log(Tooltip.init);//undefined
  console.log(Tooltip.prototype.init);//function()
  console.log(tt.init);//function()
```

Isso por que criamos inicialmente um objeto Tooltip vazio com uma função construtora .(funções também são objetos em javascript).

E, se não tivéssemos usado o prototype:

<pre class="javascript">var Tooltip =(function(){
  "use strict";

  function Tooltip() {}
  Tooltip.init = function(objs) {
    //..
  };
  Tooltip.createWrap = function(obj) {
    //..
  };
  Tooltip.getContent = function(obj) {
    //..
  };
  return Tooltip;
}());

var $ = function(selector) {
  return document.querySelectorAll(selector);
};
window.addEventListener("load", function() {
  Tooltip.init($('.tt'));
  Tooltip.init($('#another'));

  var tt = new Tooltip();
  console.log(tt.init);//undefined
  console.log(Tooltip.init);//function()
});
```

As funções existiriam somente no objeto Tooltip, e não nas instâncias dele. A menos que copiássemos explicitamente os métodos de Tooltip, para dentro da instância tt:

<pre class="javascript">tt.init = Tooltip.init;
  console.log(tt.init);//function()
```

## Nenhuma é mais ou menos correta

Não é mais correto ou menos errado. Funções construtoras ou objetos literais, cada forma de programar implica em estilos diferentes de codificar e resolve problemas, assim como alguns patterns só são implementados em um estilo e não no outro.

Fique a vontade para escolher qual forma mais lhe agrada, ou esteja pronto a continuar uma forma já definida pela sua equipe. O importante é ter em mente que existem diferentes formas de fazer uma mesma coisa, mas não mais ou menos correta por isso.

## Demonstração

Subi no github a demonstração de todos as formas de fazer esse tooltip

<https://github.com/wbruno/examples/tree/gh-pages/tt>
