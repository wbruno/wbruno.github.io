---
id: 3073
title: 'Programando Orientado a Eventos &#8211; Quiz em multipassos'
date: 2013-09-19T14:42:55+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3073
permalink: /javascript-puro/programando-orientado-eventos-quiz-em-multipassos/
dsq_thread_id:
  - "2102403692"
yst_is_cornerstone:
  - ""
categories:
  - Javascript
tags:
  - formulário
---
Apesar de programarmos javascript a muito tempo, parece que às vezes nos esquecemos que a mágica advém da interação que essa linguagem consegue fazer com o usuário. E a forma com que &#8220;ouvimos&#8221; as ações dos usuários pode ou não deixar nosso código muito confuso, grande e difícil de dar manutenção.

A minha proposta aqui, é sugerir uma organização de como tratamos os comportamentos.

[<img src="http://wbruno.com.br/wp-content/uploads/2013/09/a2.png" alt="a" width="785" height="404" class="aligncenter size-full wp-image-3092" />](http://wbruno.com.br/scripts/quiz/)
  
<!--more-->

## JavaScript é &#8220;orientado a eventos&#8221;

Montei um quiz com multipassos para mostrar como podemos **organizar nosso código javascript**, se programarmos os eventos de uma forma **orientada a comportamentos**.

A minha proposta é em vez de adicionarmos **absolutamente** tudo o que queremos diretamente nos eventos _.onsubmit_, _.onclick_, _.onkeyup_ &#8230; ou tratarmos cada objeto independente, que trabalhemos numa organização por comportamentos.

Se você ainda não respondeu, vai lá no [Quiz &#8211; Qual meu perfil como FrontEnd ?](http://wbruno.com.br/scripts/quiz/) que eu te espero aqui, para continuar falando mais sobre como organizar pensando em &#8220;comportamentos&#8221;.

## Abstraia

Meu quiz é formado por 8 passos, sendo o último responsável apenas por mostrar ao usuário o &#8220;resutado&#8221;.

Todos os passos possuem uma &#8220;validação&#8221; se foi ou não preenchido. (tente voltar ao quiz e prosseguir em qualquer um deles, sem responder o que foi perguntado).

Aqui eu abstrai esse comportamento de &#8220;validar&#8221; se já foi respondido, e adicionei um eventListener para todos os forms que mostra um erro caso não esteja preenchido, ou deixa prosseguir mostrando o próximo passo, caso esteja tudo Ok.

<pre>loop($quizForm, function ($form) {
    $form.addEventListener("submit", function (e) {
        e.preventDefault();

        if (this.getAttribute('data-answer') === 'answered') {
            //.. mostra próximo passo
        } else {
            //.. mostra um erro e não prossegue
        }

    });
});
</pre>

Acima eu faço um loop por cada uma tags <form> e adiciono um listener no evento submit de cada um deles para apenas validar a resposta do usuário.

Independente do que mais esse passo terá que fazer, ele vai precisar dessa validação.

## Adicione o que mais vc quiser

Feita a validação inicial, que era um comportamento comum a todos os formulários, eu vou especificando e adicionando os outros comportamentos específicos, como por exemplo, como decido se um passo foi ou não respondido ?

### Verificando se o passo 1 foi respondido

<pre>$formUser.addEventListener("submit", function () {
        answers.user = [];

        if ($name.value !== '' && $email.value !== '') {
            this.setAttribute('data-answer', 'answered');
        }
    });
</pre>

Lembram do IF da validação ? O meu listener anterior considera como &#8220;respondido&#8221;, se o atributo &#8220;data-answer&#8221;, estiver como &#8220;answered&#8221;. Para o passo 1, verifico se os 2 inputs foram preenchidos.

### Verificando se os demais passos foram respondidos

E para os outros passos, que são formulários com tags rádio, eu verifico se algum dos radios daquele form está marcado

<pre>var $radio = $form.querySelector('input[type="radio"]:checked');</pre>

Simples assim.

## Continue adicionando outros comportamentos

O sétimo passo, possui:
  
-> uma validação para que não deixem vazio,
  
-> uma regra para verificar se foi preenchido,
  
-> decide qual resposta mostrar,
  
-> envia um ajax

Ou seja, esse último passo possui **quatro comportamentos**, e eu separei isso em 4 chamadas de listeners do evento submit. Sério, dá uma olhada no código.

## O código

Coloquei no [meu github](https://github.com/wbruno/examples/tree/gh-pages/quiz). Me diz o que vc achou dessa maneira de programar e forka lá o projeto.. 🙂