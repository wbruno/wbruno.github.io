---
id: 2929
title: 'Afinal, como é Orientação a Objetos em JavaScript ? - Exemplos'
date: 2013-05-21T07:00:06+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2929
permalink: /javascript-puro/afinal-como-e-orientacao-a-objetos-em-javascript-exemplos/
dsq_thread_id:
  - "2100745702"
categories:
  - Javascript
tags:
  - oo
---
Como será que é a orientação a objetos no javascript ?

[<img class="aligncenter size-full wp-image-2978" alt="js-logo" src="/wp-content/uploads/2013/05/js-logo.jpg" width="800" height="341" srcset="/wp-content/uploads/2013/05/js-logo.jpg 800w, /wp-content/uploads/2013/05/js-logo-300x127.jpg 300w" sizes="(max-width: 800px) 100vw, 800px" />](/wp-content/uploads/2013/05/js-logo.jpg?a=a)

Essa linguagem mal compreendida, não possui classes, nem interfaces, não tem operadores de visibilidade e ainda por cima é baseada em prototype. Primeiro de tudo, comece se esquecendo de todos os exemplos que vc leu com <var>new Pessoa();</var>, <var>obj.prototype.carro</var>, <var>Cachorro.latir</var> ou <var>.morder</var>. Esqueça!

Eu pelo menos nunca projetei nenhum sistema web com carros, cachorros ou pessoas falantes no meu javascript.

<!--more-->



Então vamos para o nosso mundo real: sistemas web. Lá nós fazemos validações de formulários, lightboxs, tooltips, slideshows, adcasts, carouseis, requisições ajax, manipulações do dom.. entre outras coisas.

## Javascript não possui classes

E isso é ótimo para o javascript, mas também é o maior motivo das dúvidas dos programadores que já possuem experiência em outras linguagens.

### jSON

Um objeto literal em javascript é denotado por chaves <var>var tweet = {};</var>.

``` js
var tweet = {
    'user': 'tiu_uiLL',
    'message': 'Afinal, como é Orientação a Objetos em JavaScript ? – Exemplos',
    'date': '2013-05-17'
};
console.log( tweet.user );//tiu_uiLL
console.log( tweet.message );//Afinal, como é Orientação a Objetos em JavaScript ? – Exemplos
```

A variavel <var>tweet</var> é um objeto javascript. Possui 3 atributos: user, message e date.

Para acessa-los, uso o operador **ponto**. (igual a linguagem Java)

### Array de jSONs

Arrays em javascript são denotados por colchetes <var>var tweets = [];</var>.

``` js
var tweets = [
    {
        'user': 'tiu_uiLL',
        'message': 'Afinal, como é Orientação a Objetos em JavaScript ? – Exemplos',
        'date': '2013-05-21'
    },
    {
        'user': 'tiu_uiLL',
        'message': 'Plugin jQuery em elemento criado dinamicamente com javascript – append jQuery',
        'date': '2013-05-16'
    }
];
console.log( tweets[0].message );//Afinal, como é Orientação a Objetos em JavaScript ? – Exemplos
console.log( tweets[1].message );//Plugin jQuery em elemento criado dinamicamente com javascript – append jQuery
```

Arrays em javascript também começam no índice zero. Veja que bastou indicar dentro dos colchetes a posição, e depois acessei normalmente a propriedade message apenas colocando o ponto.

## O conceito

Apesar de javascript diferir das outras linguagens clássicas na forma de implementar orientação a objetos, os conceitos são os mesmos.

Um objeto é algo que possui propriedades e faz coisas. E as boas práticas que já conhecemos também são verdades. Quase tudo em javascript é um objeto, até por exemplo, funções e expressões regulares.

### Exemplo

É comum ao trabalhar com objetos em javascript, começar com um objeto em branco, ou com poucos comportamentos, e ir adicionando então o que for preciso.

Criei para ilustrar um simples tooltip. Toda a base desse tooltip é feita com css, pois ele trabalha diretamente com o pseudo seletor <var>:hover</var>. O único papel do javascript é varrer todos os elementos para qual o plugin tenha sido chamado, e então criar um wrap e inserir o conteúdo do tooltip nessa tag.

``` js
;(function(){
  "use strict";
  var tt = {};
  tt.init = function(objs) {
    var i = objs.length;
    while(i--) {
      var obj = objs[i],
        wrap = tt.createWrap(obj),
        ttContent = tt.getContent(obj);

      wrap.appendChild(ttContent);
    }
  };
  tt.createWrap = function(obj) {
    var wrap = document.createElement('span');
    wrap.className = 'tt-wrap';
    obj.parentNode.replaceChild(wrap, obj);
    wrap.appendChild(obj);
    return wrap;
  };
  tt.getContent = function(obj) {
    var rel = obj.getAttribute('data-rel');
    return document.querySelector(rel);
  };
  window.addEventListener("load", function() {
    tt.init($('.tt'));
    tt.init($('#another'));
  });
  var $ = function(selector) {
    return document.querySelectorAll(selector);
  }
}());
```

Fork lá no github <https://github.com/wbruno/examples/tree/gh-pages/tt>.

#### Sem sujeira no namespace global

Um dos maiores motivos para usarmos orientação a objetos e clousures no javascript, é não sujar o namespace global. Note que poderíamos chegar ao mesmo resultado se as funções fossem criadas diretamente:

``` js
var init = function(objs) {
```

Mas assim estaríamos colocando todos esses métodos direto no objeto window, o que poderia causar sobrescritas de comportamentos de scripts isolados dentro da nossa aplicação.

Mais ou menos, como se uma função do carousel atrapalhasse uma função de um modal, que não tem nada a ver um com o outro, mas por estarem declarados publica e globalmente sem nenhuma preocupação, interferem um no outro.

#### Objetos são coisas

Um dos princípios para pensar em orientação a objetos é pensar em coisas. Uma lixeira é um objeto, ela possui um certo tamanho e comporta uma certa quantidade de lixo, assim como poderia possuir ações, do tipo: <var>lixeira.reciclar();</var>. Mas esse método reciclar não faz sentido em uma <var>geladeira</var>, por exemplo.

Por isso que isolamos os comportamentos em objetos diferentes, e cada método possui uma única responsabilidade, para ser mais reutilizável dentro do seu próprio contexto.

## Clousures

Uma clousure define um escopo de execução. Veja por exemplo:

``` js
function init(){
  console.log('window scope');
}
(function(){
  function init(){
    console.log('local scope');
  }
  init();//local scope
  window.init();//window scope
}());
```

Declarei 2 funções com o mesmo nome: <var>init</var>. Porém cada uma em um escopo. Uma está lá no escopo global window, e outra é local dessa clousure. Por existirem em escopos diferentes uma função não interfere na outra e pode coexistir em um código.

Tudo o que for declarado no escopo window é acessível de qualquer escopo, pois window é o root.

Mas o que for declarado dentro da clousure só é acessível de dentro dela, se não for usado nenhum padrão de revelação.

``` js
(function(){
  var tt = {
    init : function() {
      console.log('namespace tt');
    }
  };
  tt.init();//namespace tt
}());
tt.init();//ReferenceError: tt is not defined
```

Isso é importante para entendermos como podemos criar módulos independentes e com visibilidades privadas para usarmos em nossos sistemas.

## Module pattern

O problema da minha primeira implementação é que a invocação tem que ficar dentro da clousure, pois como vimos acima, o método tt.init(), não está definido fora da clousure. Para corrigir isso, e fazer nosso código ser usável, usamos o module pattern.

A implementação ficaria assim:

``` js
var tt = (function(){
  "use strict";
  var tt = {};

  tt.createWrap = function(obj) {
    //..
  };
  tt.init = function(objs) {
    //..
  };
  tt.getContent = function(obj) {
    //..
  };

  return {
    init : tt.init
  };
}());

var $ = function(selector) {
  return document.querySelectorAll(selector);
};
window.addEventListener("load", function() {
  console.log(tt);//Object { init=function()}
  console.log(tt.createWrap);//undefined
  tt.init($('.tt'));
  tt.init($('#another'));
});
```

Agora posso usar o módulo tt(tooltip) de qualquer lugar da minha aplicação, sabendo que o único método visível é o <var>.init()</var>.

Os 2 códigos estão no <a href="https://github.com/wbruno/examples/tree/gh-pages/tt" rel="nofollow">https://github.com/wbruno/examples/tree/gh-pages/tt</a>. Por hora vou parando aqui, mas usarei o mesmo git para colocar exemplos de outros patterns e para quando eu for escrever sobre herança.

E ai? ficou um pouco mais claro o que vem a ser orientação a objetos em javascript ?
