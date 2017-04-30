---
id: 1788
title: 'Flash chamando função javascript, e javascript chamando função do flash &#8211; ExternalInterface'
date: 2012-02-22T13:37:05+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1788
permalink: /javascript-puro/flash-chamando-funcao-javascript-javascript-chamando-funcao-flash-externalinterface/
categories:
  - Javascript
---
Boas galera!

Precisei disso recentemente, e como não trabalho muito com flash, e nunca programei nada de verdade em ActionScript, pedi socorro ao mestre do flash: **Thiago Cruz**.

No blog dele, ele já postou ótimos exemplos, de <a href="http://berseck.wordpress.com/2009/03/25/utilizando-classe-externalinterface-as2/" target="_blank" title="Utilizando classe externalInterface() AS2">utilizar a class externalinterface</a>, então deixo por aqui também, o exemplo do código fonte que ele fez para mim.
  
<!--more-->


  
O **javascript** fica assim:

<pre name="code" class="javascript">function onFlashReady() {
    sendToAS("another test message");
}

function callJS(value) {
    onFlashReady();
    return "Hi Flash.";
}

function thisMovie(movieName) {
    if (navigator.appName.indexOf("Microsoft") != -1) {
        return window[movieName];
    } else {
        return document[movieName];
    }
}

function sendToAS(value) {
    thisMovie("externalclass").callAS(value);
}
</pre>

e o **action script**:

<pre name="code" class="javascript">import flash.external.*;

play();

System.security.allowDomain("*");

ExternalInterface.addCallback("callAS", this, func);
ExternalInterface.call("callJS", 1);

function func(n:Number) {
    gotoAndStop(n);
}
</pre>

## <a href="http://wbruno.com.br/scripts/externalclass.zip" target="_blank">Download ExternalClass.zip</a>

Vlw pela ajuda Thiago!!