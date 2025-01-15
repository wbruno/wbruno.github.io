---
id: 3021
title: 'Review Livro: Object-Oriented JavaScript. Create scalable, reusable high-quality JavaScript applications, and libraries'
date: 2013-06-13T07:00:11+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3021
permalink: /livro/livro-object-oriented-javascript-create-scalable-reusable-high-quality-javascript-applications-and-libraries/
categories:
  - Livro
tags:
  - review
---
[<img src="/wp-content/uploads/2013/06/object-oriented-javascript-create-scalable-reusable-high-quality-javascript-applications-and-libraries_2640_500.jpg" alt="object-oriented-javascript-create-scalable-reusable-high-quality-javascript-applications-and-libraries_2640_500" width="243" height="300" class="aligncenter size-full wp-image-3022" />](/wp-content/uploads/2013/06/object-oriented-javascript-create-scalable-reusable-high-quality-javascript-applications-and-libraries_2640_500.jpg)

**Object-Oriented JavaScript** é com certeza o assunto que mais divide e confunde os desenvolvedores iniciantes nos dias de hoje. Sim, javascript é orientado a objetos. Não possui classes pq não precisa, e prototype é mais simples do que parece.

Livro do Stoyan Stefanov publicado pela packt publishing.

<!--more-->

## Opinião Geral

Esse é daqueles livros que vc terá que ler diversas vezes até entendê-lo completamente. Mas isso pq o livro abre a nossa cabeça, estendendo nossa visão sobre javascript.

O autor é desenvolvedor no yahoo e os revisores do livro são só os caras mais fodas do mundo nessa linguagem. A minha edição é a original em inglês, portanto não posso opiniar sobre a tradução, se é que existe.

Por falar muito bem dos conceitos esse livro é ótimo para quem quer iniciar no javascript, ou precisa melhorar suas skills, fundamentando conhecimento.

## Capítulo 1 - Introdução

A organização do livro é impecável. Este capítulo começa com um motivacional e um texto dizendo que o livro começa do zero, sem pressupor nenhum conhecimento prévio sobre programação do leitor.

O foco do livro é a linguagem javascript, mas explica conceitos de programação que não são exclusividades do js, falando até sobre classes que é algo que não existe em js. Capítulo curto, então indico a leitura dele para ir pegando &#8220;o ritmo da leitura&#8221;.

## Capítulo 2 - Tipos primitivos

Eu sempre leio os meus livros sem pular nada, mesmo que algumas páginas falem sobre coisas que já sei. Sempre há algo para aprender ou relembrar. Mas se você já estiver realmente seguro sobre variáveis, operações e tipos, pode pular sem culpa.

O capítulo termina com exercícios. Então se vc não conseguir respondê-los volte e leia o capítulo. =)

## Capítulo 3 - Funções

JavaScript faz muita mágica com as funções, então é preciso entendê-las bem. Esse capítulo começa falando sobre as nativas e explicando do básico como funciona.

Na página 72 da minha edição há o subcapítulo **Functions are Data**. Comece a prestar mais atenção a partir daqui.

```function f(){return 1;}
var f = function(){return 1;}
```

Função que retorna função e clousures são tópicos que vou escrever posts sobre, pois fazem parte da parte boa do javascript.

## Capítulo 4 - Objetos

Um dos capítulos mais importantes, vai da página 93 até a 148.

Uma diferença prática entre objetos literais (jSON) e aqueles criados com funções construtoras é que por causa do new que temos que usar para instanciar novos objetos criados com funções, cada uma das instâncias podem ser diferentes entre si. Enquanto para fazer isso com objetos literais, teríamos que copiar todo o objeto em outra variavel.

Ainda fala sobre alguns objetos nativos da linguagem como Number, String e Date.

## Capítulo 5 - Prototype

Explicando prototype com exemplos e desde o princípio, preste bastante atenção nesse capítulo, pois esse é o assunto em que os desenvolvedores mais demoram para entender sobre javascript.

O capítulo é bem curto, então releia ele.

## Capítulo 6 - Herança

A explicação de herança aqui é específica da linguagem, e exatamente por isso o livro é ótimo. Pois é focado. Vamos continuar lendo sobre prototype, mas isso é pq é assim q funciona herança no js.

## Capítulo 7 - O ambiente do navegador

Eu trabalho com web, então o ambiente do meu js são os browsers. Este capítulo fala sobre o objeto window e DOM, como inserção e os métodos getElement(s)?By&#8230;

Não é um capítulo de leitura obrigatória se vc tiver sem paciência, mas ele é curto, então vale a pena ler para relembrar algumas coisas.

## Capítulo 8 - Código e padrões de projeto

Esse último aqui fala sobre como melhorar seu código com namespace, chaining, métodos privados e privilegiados (visibilidade). E ai começam os padrões Singleton, Factory, Decorator e Observer.

Esse capítulo tem cerca de 25 páginas. Depois dele é só apêndice e índice.
