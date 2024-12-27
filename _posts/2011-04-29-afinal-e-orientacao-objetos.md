---
id: 846
title: Afinal o que é Orientação a Objetos ?
date: 2011-04-29T00:07:01+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=846
permalink: /opiniao/afinal-e-orientacao-objetos/
dsq_thread_id:
  - "2101309435"
categories:
  - Opinião
tags:
  - oo
---
Antes de entendermos **o que é**, precisamos entender **como**, **porque** e **para que** surgiu.

<!--more-->

## Como

Foi aos poucos. Sempre que lemos textos sobre OO, vemos citações sobre smalltalk[ apesar de pelo menos eu, nunca ter visto uma linha de código nessa linguagem]. Continuamos as leituras e pesquisas, e vemos que outras linguagens, já adotavam alguns principios desse paradigma, algumas outras como C e php, lhe deixam programar tanto em OO, como apenas de forma estruturada, Java somente em OO&#8230;

## Porque

> &#8216;Para aproximar o mundo real do mundo virtual&#8217;.

Resumido não ?

O difícil é enfiar isso na cabeça dos programadores de hoje em dia. É isso gente, pronto. Daqui é que derivam as outras coisas de OO, mas o porque é este.

## Para que

Para principalmente ajudar a _padronizar o desenvolvimento_. Discordo das afirmações que dizem que _todo código escrito com o paradigma de programação estruturada, é uma bagunça._. Existem <a href="https://wbruno.com.br/opiniao/diferenca-entre-cara-programa-um-programador/" target="_blank">programadores e caras que programam.</a>.

Para os **CQP**s, não importa se é orientado a objetos, a eventos, a <a href="http://pt.wikipedia.org/wiki/Paradigma_de_programa%C3%A7%C3%A3o" target="_blank">qualquer outra coisa</a>, vai ficar ruim e pronto. Eu diria até que um **CQP** fazendo OO, é tão ou mais perigoso do que ele fazendo estruturado.

Entendam por favor:

> Para programar OO direito e corretamente, é **necessário** saber programar de forma estruturada !

[podem comentar, estou pronto para rebater todas as críticas que essa minha frase vai gerar.]

## O que não é

OO não é Identação, isso já existia muito antes, e sempre devemos fazer, não importa o paradigma.

OO não é Reutilização, o conceito de **function**, já existia antes de OO. Okay, OO também provém reutilização, mas isso não é exclusivo desse paradigma.

É possível até conseguirmos um certo nível de poliformismo e herança usando apenas funções de linguagens estruturadas.

OO não é Organização, essa deve ser a obrigação de todo programador.

## O que é

Na minha concepção, e com as minhas palavras, o **paradigma de orientação a objetos**, foi projetado para obrigar _programadores diferentes que não se conhecem, e não possuem acesso total ao código um dos outros_, a programarem de uma _forma organizada_, e conforme foi _definido no projeto_. Vai além do UML.

Para que uma equipe de vários programadores consigam trabalhar juntos, sem interferir, ou comprometer completamente o restante da aplicação com erros pontuais.

Um é capaz de servir funcionalidades e usar as de outro programador, sem conhecer como foram implementadas.

Basicamente, foi isso que os outros paradigmas não conseguiram resolver.

OO possui ferramentas, como <a href="https://wbruno.com.br/php/afinal-e-interface-oop/" target="_blank">Interfaces</a> e Classes Abstratas, que fazem exatamente isso. Definem um padrão a ser seguido.

Foi aqui que ouvi uma crítica: &#8220;Ahh, mas se o cara **quiser mesmo**, ele não vai nem implementar a interface, e nem extender a abstract, e assim então vai conseguir programar da forma dele, fugindo do padrão&#8221;.

Só tenho uma resposta para isso: esse cara não deveria estar nessa profissão. Pronto.

O padrão tá alí, e o paradigma, oferece mecanismos muito bons, para auxiliar o desenvolvimento. Se o cara quer realmente fazer merda, então ele não deveria ser programador. Não é questão de &#8216;pressa&#8217;, pois já que seguindo o que está pronto, obteremos ganhos de produtividade, se a base tiver sido bem feita.

## Códigos devem ser escritos para humanos

Todos já ouvimos essa frase. É exatamente isso que OO faz. Tem algo mais &#8216;humano&#8217; e próximo de nós do que os **objetos**, que nos rodeiam ?

O que deve mudar para que consigamos trabalhar com OO, é a forma de pensar.

Precisamos modelar nossas classes, como objetos reais. Precisamos entender oque deve ou não pertencer a cada <a href="https://wbruno.com.br/sql/afinal-o-que-e-entidade/" target="_blank">Entidade</a> nossa. Numa tradução livre que fiz, no dia em que fui apresentado a este paradigma:

Um objeto possui qualidades(adjetivos mesmo!) e faz coisas. Estou olhando para uma lâmpada agora.

A minha lâmpada é:

-> branca [qualidade]

-> de 50w [qualidade]

-> pequena [qualidade]

-> cilindrica [qualidade]

A minha lâmpada pode:

-> ficar acessa [faz]

-> ficar apagada [faz]

-> queimar [faz]

.. e sei lá até onde o joguinho do **pensar simples** pode te levar.

As _qualidades_ alí, são os **atributos** dos nossos objetos, e as _coisas que ele faz_, são os **métodos** dele. A minha lâmpada, precisa de um **interruptor** para funcionar, e esse interruptor, ao ser _apertado pelo usuário_, vai abrir ou fechar o circuito da rede elétrica.

abrirCircuito, e fecharCircuito são os métodos do meu objeto interruptor. A lâmpada não sabe como o interruptor vai fechar o circuito e fornecer corrente elétrica para ela ficar acessa, ela apenas sabe que se o interruptor fizer uma coisa, a lâmpada terá que fazer outra. O Interruptor, não sabe se a lâmpada tá queimada ou boa, ele vai enviar a informação mesmo assim. Lá na frente é que precisa disparar o Exception.

Dependendo da informação que ele enviar, a lâmpada ficará acesa ou apagada.

Isto é orientação a objetos. Um objeto conversando com o outro.

Okay, exemplo tosco, mas nem todo mundo enxerga isso. E vejo diariamente vários programadores, que não possuem esses conceitos incorporados a eles, e **desembestam a escrever classes**, achando que estão programando em OO.

Nunca pararam para pensar o porque da palavra **orientação**, no nome.

OO veio para ajudar, reforçando várias coisas que já existiam, e forçando-nos a sermos coerentes.

Isso é OO.
