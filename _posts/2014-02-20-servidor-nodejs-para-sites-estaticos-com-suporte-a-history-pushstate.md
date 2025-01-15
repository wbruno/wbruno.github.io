---
id: 3265
title: Servidor NodeJS para sites estáticos, com suporte a history.pushState
date: 2014-02-20T23:00:59+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3265
permalink: /nodejs/servidor-nodejs-para-sites-estaticos-com-suporte-a-history-pushstate/
categories:
  - NodeJS
---
<img src="/wp-content/uploads/2014/02/nodejs-wallpaper-nsfw.jpg" alt="nodejs-wallpaper-nsfw" width="800" height="271" class="aligncenter size-full wp-image-3268" />

<!--more-->



Já vimos diversas vezes como fazer um servidorzinho básico em NodeJS, usando o Express

## Hello World

``` js
var express = require('express'),
    app = express();

app.get('/', function(req, res) {
    res.send('index');
});

app.listen(3003);
```

Além disso, podemos pedir para que uma view seja renderizada:

``` js
app.get('/', function(req, res) {
    res.render('index', { title: "My Site" });
});
```

Mas e se **quando o servidor recebesse uma requisição ajax**, o Node retornasse um **jSON**, no lugar do HTML completo da página, que está cheio de coisas que não queremos (template, tag head, &#8230;) ?

Ai otimizaríamos essas requisições, pois o json já parseado do servidor, viria apenas com o conteúdo e título da página, economizando banda, e processamento, pois não precisaríamos mais fazer o parser do html inteiro no client-side.

Ficando assim, bem mais legal de se trabalhar com <var>history.pushState</var>. Veja:

``` bash
content.innerHTML = json.content;

history.pushState(href, json.title, href);

document.title = json.title;
document.querySelector("meta[name='description']").setAttribute("content", json.description);
```

Que tal ?

## Forka lá no Github!

Foi exatamente isso que eu fiz nesse projeto no meu github. Dá uma olhada lá: [wbruno / static-server-ajax](https://github.com/wbruno/static-server-ajax)

## Exemplo online

Hospedei no meu cloud, para vocês poderem verificar as requisições e o pushState

<a href="http://node.wbruno.com.br/" rel="nofollow">http://node.wbruno.com.br/</a>.

## Palestra de graça na Eventials

Apesar do foco não ser NodeJS, vou utilizar esse &#8220;servidorzinho&#8221;, durante a palestra [JavaScript - Boas práticas e otimizações](https://www.eventials.com/pinceladasdaweb/javascript-boas-praticas-e-otimizacoes/), onde a idéia principal é mostrar maneiras diferentes de programar em javascript client-side, entendendo o que elas fazem, e quais devemos preferir.

É a minha primeira palestra online, então o conteúdo começará do básico, mas não será nada raso. =)
