---
id: 3218
title: Validando formulários apenas com html5
date: 2014-02-18T08:00:55+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3218
permalink: /html/validando-formularios-apenas-com-html5/
categories:
  - HTML
tags:
  - formulário
  - html5
---
<img src="http://wbruno.com.br/wp-content/uploads/2014/02/html5.jpg" alt="html5" width="800" height="354" class="aligncenter size-full wp-image-3262" />

Validar formulários é chato, tedioso e trabalhoso. Felizmente alguém olhou isso e resolveu incluir dentro da especificação do html, alguns atributos e valores novos muito interessantes.

Se usarmos corretamente, e estudarmos Expressões Regulares, é possível fazer uma validação simples sem escrever nenhuma linha de javascript. Vou deixar abaixo alguns snippets da tag input, utilizando o type correto (veja aqui todos os <a href="http://html5doctor.com/html5-forms-input-types/" rel="nofollow">types novos da html5</a>) e um uso do atributo **pattern** para os qual eu escrevi algunms ERs.
  
<!--more-->


  
**Apenas letras**

<pre>&lt;input type="text" required="required" name="text" pattern="[a-z\s]+$" /></pre>

**Apenas números**

<pre>&lt;input type="text" required="required" name="numbers" pattern="[0-9]+$" /></pre>

**Data**

<pre>&lt;input type="date" required="required" maxlength="10" name="date" pattern="[0-9]{2}\/[0-9]{2}\/[0-9]{4}$" min="2012-01-01" max="2014-02-18" /></pre>

**Hora**

<pre>&lt;input type="time" required="required" maxlength="8" name="hour" pattern="[0-9]{2}:[0-9]{2} [0-9]{2}$" /></pre>

**Campos genéricos de texto**

<pre>&lt;input type="text" required="required" name="name" /></pre>

**Telefone**

<pre>&lt;input type="tel" required="required" maxlength="15" name="phone" pattern="\([0-9]{2}\) [0-9]{4,6}-[0-9]{3,4}$" /></pre>

**Email**

<pre>&lt;input type="email" required="required" class="input-text" name="email" pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}$" /></pre>

**Moeda**

<pre>&lt;input type="tel" required="required" maxlength="15" name="valor" pattern="([0-9]{1,3}\.)?[0-9]{1,3},[0-9]{2}$" />
</pre>

Utilizei o type=&#8221;tel&#8221;, pq em celulares renderiza melhor o teclado.

**Input file**

<pre>&lt;input type="file" name="file" accept="image/*" required="required" /></pre>

## placeholder

Lembre-se de usar o placeholder nos seus campos em que você precise _&#8220;dar alguma dica&#8221;_ para o usuário de como ele deve preenchê-lo

## Estilizar os inputs

Faça testes utilizando as pseudo classes

<pre>input:required:invalid {}
input:required:valid {}</pre>

## Personalizar as mensagens de erro

Encontrei este artigo bem completo e interessante: <a href="http://blog.popupdesign.com.br/validando-formularios-like-a-boss-com-html5/" rel="nofollow">Validando formulários like a boss com HTML5</a>. Onde é mostrado o atributo: <var>required x-moz-errormessage=&#8221;Ops. Não esqueça de preencher este campo.&#8221;</var>, logicamente exclusivo do Firefox.

E para webkit, o css:

<pre>::-webkit-validation-bubble {/*Insira aqui seu CSS.*/}
::-webkit-validation-bubble-message {}
::-webkit-validation-bubble-arrow {}
::-webkit-validation-bubble-arrow-clipper {}</pre>

## That&#8217;s all folks!

Em alguns inputs, mesmo com o type definido, eu forcei a validação no pattern, pois um pode ser implementado sem o outro pelos browsers, e existe um &#8220;bug&#8221; no type email, em que no Chrome ele aceita um email do tipo: **email@a**, sem obrigar que o cliente informe o domínio do site. (.com, .net&#8230;)

Comente caso use algum, ou tenha outro para sugerir!!