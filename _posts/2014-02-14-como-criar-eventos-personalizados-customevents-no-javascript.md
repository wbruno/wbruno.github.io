---
id: 3060
title: Como criar eventos personalizados (CustomEvents) no JavaScript
date: 2014-02-14T08:00:59+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3060
permalink: /javascript-puro/como-criar-eventos-personalizados-customevents-no-javascript/
categories:
  - Javascript
---
JavaScript é uma linguagem **orientada a eventos**. JavaScript é uma linguagem **orientada a eventos**. JavaScript..

Ok.. acho que já deu para entender.

<img src="/wp-content/uploads/2013/05/js-logo.jpg" alt="js-logo" width="800" height="341" class="aligncenter size-full wp-image-2978" srcset="/wp-content/uploads/2013/05/js-logo.jpg 800w, /wp-content/uploads/2013/05/js-logo-300x127.jpg 300w" sizes="(max-width: 800px) 100vw, 800px" />

<!--more-->

## Eventos

JavaScript é um dialeto ECMAScript, orientado a objetos, com suporte a programação funcional, e também, podemos dizer que js é **orientado a eventos**.

Afinal de contas, o browser nos avisa qndo: o dom termina de carregar, qndo uma imagem está pronta, qndo o usuário clica em algo, qndo passa o mouse em algum elemento, qndo sai de algum campo, pressiona uma tecla&#8230;

Todos esses **quandos** são eventos. E no js, lemos como:

<var>onload, onkeypress, onkeyup, onkeydown, onclick, onchange, onblur, onfocus, onmouseover, onmouseout&#8230;</var>

Mas esse lado &#8220;orientado a eventos&#8221; do javascript, ainda é mal compreendido. Não adianta programarmos JS como se fosse Java. Existem particularidades da linguagem que a fazem ser muito versátil, e é isso que devemos aprender a usar.

[Programando Orientado a Eventos](http://wbruno.com.br/javascript-puro/programando-orientado-eventos-quiz-em-multipassos/).

## CustomEvents

Além dos eventos disparados pelo usuário e browser, podemos criar os nossos próprios eventos customizados!

Isso nos ajudará a manter um código mais organizado e mais condizente com o propósito da linguagem que estamos usando. É natural pensarmos que &#8220;quando o usuário clicar em um botão, ou quando ele trocar de certo campo, tal coisa deve ser acionada&#8221;.

Mas e se além dos eventos disparados pelo user e pelo browser, o nosso próprio código disparasse eventos nos informando que algo aconteceu ?

É exatamente esse o propósito do CustomEvents.

Eu creio que usar isso ajudará na organização do código, ajudando a evitar o temido <a href="http://callbackhell.com/" rel="nofollow">Callback Hell</a>, desde que paremos de pensar nas outras tantas linguagens de programação que sabemos, e passemos a pensar em javascript.

Para quem sabe Design Patterns, creio que vc pode pensar que é um Observer nativo.

## Código

``` html
<div id="t"></div>
<script>
var myElement = document.getElementById("t");
myElement.addEventListener("userLogin", function(e) {
    console.info("Event is: ", e);
    console.info("Custom data is: ", e.detail);
});

// First create the event
var myEvent = new CustomEvent("userLogin", {
    detail: {
        username: "davidwalsh"
    }
});

// Trigger it!
myElement.dispatchEvent(myEvent);
</script>
```

Retirei o trecho de código acima daqui: [JavaScript CustomEvent](http://davidwalsh.name/customevent)

Achei que não tinha sentido rescrever um código tão simples, e não citar a fonte, até pq lá explica bem como fazer. A idéia desse meu post, é mais pensar sobre **porque** e **quando** usar.
