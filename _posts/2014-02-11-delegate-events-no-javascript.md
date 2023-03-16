---
id: 3001
title: Delegate Events no JavaScript
date: 2014-02-11T08:00:14+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3001
permalink: /javascript-puro/delegate-events-no-javascript/
categories:
  - Javascript
tags:
  - boas práticas
  - dom
---
É engraçado procurar os termos: **delegate events** e **delegate javascript** e então comparar os artigos escritos em inglês com os escritos em português.

## Artigos em inglês

Mostram como o delegate funciona por baixo dos planos, mostrando códigos.

## Artigos em português

Apenas comparam as funções .bind(), .live(), .delegate() e .on(). Teve só um que só citou como funciona.
  
<!--more-->


  
A idéia é **delegar** a responsabilidade de escutar eventos a um ou mais elementos, ao elemento pai daquele elemento.

Isso é muito útil por diversos motivos.

## Evitar sobrecarga de manipuladores no DOM

Imagine uma lista de itens, com mais de 20 tags LI. Colocando um evento click em cada tag LI, temos 20 listeners do evento, um para cada tag. Isso deixa o processamento da página lento, pois apesar de todas as otimizações dos motores, imagine com mais elementos, qntas vezes é necessário aplicar o addEventListener..

## Atrelar eventos em elementos criados dinamicamente

E aqui, podemos citar duas situações em que isso ocorre. Seja quando duplicamos uma linha de uma tabela, ou adicionamos mais inputs a um formulário, ou quando trazemos via ajax um html, e o inserimos dinamicamente no DOM.

Por esses elementos não existirem ainda no DOM no momento em que o DOMContentLoaded foi disparado, então o listener do evento não foi atrelado a eles. E é ai que o delegate ajuda a dar vida as funções que precisamos.

O mesmo trabalho do .live(), e do .on() do jQuery quando aplicado com a sintaxe do .delegate(). Só que com javascript puro, por baixo dos panos, e entendendo o que está acontecendo.

## Como funciona?

Aproveitando o eventBubble do javascript, em que um click em um elemento filho, dispara um click no elemento pai, usamos para testar se o **alvo** do click, foi o elementos que estamos procurando.

A função .live() fazia um delegate diretamente no objeto <var>document</var>, pois o click de todos os elementos da nossa página, propaga até chegar no root. Dessa forma era super simples de usar (não era necessário indicar qual o pai do elemento).

Não é uma boa prática esperar tantos eventos em um só manipulador, e o live foi depreciado do core do jQuery. 

## Nativamente

Eu estendi o prototype do objeto Element para criar nativamente suporte ao delegate, deixando uma sintaxe prática, com apenas as linhas de código abaixo:

```Element.prototype.is = function(elementSelector) {
    switch(elementSelector[0]) {
        case ".":
            var er = new RegExp(elementSelector.replace(".", ""));
            return this.className.match(er);
            break;
        case "#":
            return this.getAttribute("id") === elementSelector.replace("#", "");
            break;
        default:
            return this.tagName === elementSelector.toUpperCase();
            break;
    }
};
Element.prototype.delegate = function(eventName, elementSelector, cb) {
    var $this = this;

    $this.addEventListener(eventName, function (evt) {
        var $this = evt.target;

        if ($this.is(elementSelector)) {
            cb.call($this, evt);
        }
        if ($this.parentNode.is(elementSelector)) {
            cb.call($this.parentNode, evt);
        }
    });
};
```

A forma de uso é simplesmente:

```document.getElementById('menu').delegate('click', 'li', function(event){
    console.log(this.innerHTML);
});
```

=)