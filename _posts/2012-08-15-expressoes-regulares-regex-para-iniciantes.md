---
id: 2403
title: 'Expressões Regulares &#8211; REGEX para iniciantes'
date: 2012-08-15T07:10:39+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2403
permalink: /expressao-regular/expressoes-regulares-regex-para-iniciantes/
dsq_thread_id:
  - "2100774624"
categories:
  - Expressão Regular
---
Regular Expressions, RE, REGEX, Expressões Regulares, ER&#8230; ou aquelas letrinhas e símbolos dentro de colchetes e parênteses que não fazem o menor sentido, mas aparecem em diversos lugares quando estamos programando, seja em php, em javascript..

[<img src="/wp-content/uploads/2012/08/regex.jpg" alt="" title="regex" width="600" height="400" class="aligncenter size-full wp-image-2414" srcset="/wp-content/uploads/2012/08/regex.jpg 600w, /wp-content/uploads/2012/08/regex-300x200.jpg 300w" sizes="(max-width: 600px) 100vw, 600px" />](/wp-content/uploads/2012/08/regex.jpg)

<!--more-->



A maioria das linguagens de programação atuais possuem um interpretador de regex nativo. As **Expressões Regulares** são um conjunto de caracteres que fazem praticamente milagre quando se trata de _encontrar, selecionar ou testar_ padrões de texto em um dado conteúdo.

Todos nós já precisamos usar ou já vimos em algum lugar coisas como:

``` js
var er = /^[a-zA-Z0-9][a-zA-Z0-9\._-]+@([a-zA-Z0-9\._-]+\.)[a-zA-Z-0-9]{2}/;
```

Porém, não é legal usarmos essas letrinhas mágicas sem realmente entender o que são.

Esta regex acima, por exemplo, eu uso para [verificar se o usuário digitou um endereço de email](http://wbruno.com.br/2011/07/20/verificar-email-expressao-regular-javascript/ "Validar endereço de Email com regex em javascript") corretamente.

## Escrevendo a sua primeira regex

Vamos começar com algo bem básico:

``` php
<?php

$pattern = '/O rato roeu a roupa do rei de Roma/';
$subject = 'O rato roeu a roupa do rei de Roma';
preg_match( $pattern, $subject, $matches );

echo '<pre>';
var_dump( $matches );
```

A saída será:

``` bash
array(1) {<br />
  [0]=><br />
  string(26) "O rato roeu a roupa do rei de Roma"<br />
}<br />
```

ou seja, _casamos_(encontramos) perfeitamente todo o padrão(<var>$pattern</var>), dentro do conteúdo(<var>$subject</var>). Óbvio, pois o meu pattern é exatamente igual ao meu subject.

### Casando rato ou gato

Vou começar a &#8220;complicar&#8221; um pouquinho.. digamos que eu queira &#8220;casar&#8221;, tanto quanto for um <span style="font-weight: bold">rato</span>, como quando for um <span style="font-weight: bold">gato</span> a ter roido a tal roupa.

Agora a minha expressão regular, é assim:

``` php
$pattern = '/O (gato|rato) roeu a roupa do rei de Roma/';
```

O caracter _pipe_ &#8220;|&#8221;, representa o operador lógico OU.

Com essa er, consigo casar tanto o conteudo: <var>O <strong>rato</strong> roeu a roupa do rei de Roma</var>, quanto o conteúdo <var>O <strong>gato</strong> roeu a roupa do rei de Roma</var>.

## (rato|gato)

Essas duas palavras são bem próximas uma da outra, a única diferença é a primeira letra.

Então podemos melhorar a nossa ER, para o seguinte:

``` php
$pattern = '/O (g|r)(ato) roeu a roupa do rei de Roma/';
```

O interpretador ao ler esta regex, faz o seguinte:

-> Case a frase que começar com uma letra O maiúscula;

-> Um espaço em branco;

-> Uma letra &#8220;g&#8221; ou uma letra &#8220;r&#8221;, seguida da string &#8220;ato&#8221;;

-> Um espaço em branco&#8230;

Continua casando, sem nenhuma perda:

<var>array(3) {<br /> [0]=><br /> string(26) &#8220;O rato roeu a roupa do rei de Roma&#8221;<br /> [1]=><br /> string(1) &#8220;r&#8221;<br /> [2]=><br /> string(3) &#8220;ato&#8221;<br /> }</var>

As posições 1 e 2 desse array, apareceram por causa dos grupos que usei na ER (aqueles trechos do <var>$pattern</var> que está dentro de parânteses), mas isso não é importante agora. Apenas note que continuo casando a mesma frase na posição 0 deste array.

## roeu ou comeu

Não sei ao certo, se o nosso gato ou rato, comeu ou roeu a roupa do pobre coitado do rei.

Mas posso adequar a expressão regular para encontrar o meliante, de acordo com o crime dele, seguindo a mesma regra do OU que usei para casar rato ou gato.

``` php
$pattern = '/O (g|r)(ato) (roeu|comeu) a roupa do rei de Roma/';
```

Com esta modificação na ER, agora consigo casar as frases:

O rato roeu a roupa do rei de Roma;

O rato comeu a roupa do rei de Roma;

O gato roeu a roupa do rei de Roma;

O rato comeu a roupa do rei de Roma.

## Aos poucos

Não tente logo de cara fazer a ER mais complexa do mundo. Comece do simples.

Vá entendendo aos poucos e melhorando a sua regex conforme for precisando.

``` php
<?php

$pattern = '/O (g|r)(ato) (r|c)om?eu a roupa d(o rei|a rainha) d(e Roma|a Belgica)/';
$subject = 'O rato roeu a roupa do rei de Roma';
preg_match( $pattern, $subject, $matches );

echo '<pre>';
var_dump( $matches );


$subject = 'O gato comeu a roupa da rainha da Belgica';
preg_match( $pattern, $subject, $matches );

echo '<pre>';
var_dump( $matches );
```

Ah, é&#8230; eu queria falar sobre a rainha da Belgica, mesmo sem saber se a Bélgica tem rainha..

Num próximo post sobre ER vou mostrar alguns casos de uso, e explicar a construção da expressão regular, passo a passo. Apartir do pensamento na necessidade.

Curtiu ? comente.
