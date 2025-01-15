---
id: 337
title: 'Criando um plugin jQuery - parte 2 - Codificando'
date: 2011-03-25T07:00:10+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=337
permalink: /jquery/criando-um-plugin-jquery-parte-2-codificando/
dsq_thread_id:
  - "2114858069"
categories:
  - jQuery
tags:
  - framework
  - plugin
---
Opa! para não perdermos o foco, vamos manter em mente a situação inicial:

**Problema:**

> &#8220;<cite>Possuo campos input em um formulário, onde dentro deles existe uma descrição do que o usuario deve digitar ali.<br /> Gostaria que quando o usuário entrasse nesse campo(clicasse, tentasse preencher..), esse valor default fosse apagado.<br /> Porém, se o usuário sair deste campo, sem escrever nada, esse valor &#8216;default&#8217;, deve voltar a aparecer. Sendo que se ele preencher, fique lá o que ele digitou.</cite>&#8220;

[Começamos](https://wbruno.com.br/jquery/criando-um-plugin-jquery-parte-1-comecando/), criando a estrutura, agora vamos codificar, para &#8220;resolver mesmo&#8221; o problema.

> &#8220;<cite>Gostaria que quando o usuário entrasse nesse campo(clicasse, tentasse preencher..), esse valor default fosse apagado.</cite>&#8220;

Como estamos programando numa linguagem client-side, &#8216;orientada a eventos&#8217;, precisamos identificar qual evento vamos usar.

<!--more-->

O trecho:

> _quando o usuário entrasse nesse campo_

, significa para nós e para o javascript, o evento **onFocus**

E o trecho

> _esse valor default fosse apagado_

significa para o javascript: atribuir um VAZIO para o atributo .value do input.

Logo, em código, isso é:

``` js
$("input[name='telefone']").focus(function(){
    $( this ).val( '' );
  });
```

Não precisamos de muito, e já resolvemos a primeira parte. Bastou entender o que tínhamos que fazer, organizar de forma lógica, e ir fazendo.

Continuando:

> _se o usuário sair deste campo_

. De novo, precisamos identificar o evento, agora estamos falando do **onBlur**.

> _sem escrever nada_

, significa testarmos o atributo **.value** do nosso objeto input, e vermos se tem algo ou não lá. Em sintaxe jQuery, possuimos o método **.val()**, para acessar esse atributo HTML do input.

> _esse valor &#8216;default&#8217;, deve voltar a aparecer_

, significa, atribuirmos novamente aquela mensagem ao nosso value.

``` js
$("input[name='telefone']").blur(function(){
    if( $( this ).val() == '' )
      $( this ).val( 'Digite seu telefone' );
  });
```

Hora de testar oque já fizemos (tudo junto):

``` html
<script type="text/javascript"> type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  /* para o input telefone */
  $("input[name='telefone']").focus(function(){
    $( this ).val( '' );
  });
  $("input[name='telefone']").blur(function(){
    if( $( this ).val() == '' )
      $( this ).val( 'Digite seu telefone' );
  });
});
</script>

  <input type="text" name="telefone" value="Digite seu telefone" />
  <input type="text" name="email" value="Digite seu e-mail" />
```

Bacana, aparentemente, estaria tudo pronto.

Mas daí notamos um bug!

Vamos ao fluxo:

> _O cara vê o input, tem algo escrito lá. OK

> Ele clica no input para escrever, nesse momento o que estava lá some. OK

> Ele escreve algo e sai do input, oque ele escreveu permanecesse. OK

> Ele clica novamente no input [e aqui acontece o bug], e oque ele tinha escrito some! BUG_

Essa última interação não estava prevista, e é por isso que precisamos testar os script enqnto estamos desenvolvendo.

Esse bug nos revela, que estamos apagando o conteudo do input, sem nos importar com oque estava escrito alí. Enquanto que isso só deveria ocorrer, se oque estivesse alí, fosse a nossa mensagem default. (afinal queremos que o usuário possa digitar e alterar oque ele quiser, mas não que ele envie nossa mensagem default para a gente).

Outro simples IF, e resolvemos esse &#8216;bug&#8217;:

``` js
$("input[name='telefone']").focus(function(){
    //só vai apagar se for igual a mensagem default
    if( $( this ).val()=='Digite seu telefone' )
      $( this ).val( '' );
  });
```

Parabéns, tecnicamente, resolvemos o problema. Do início ao fim.

Só que se precisarmos aplicar essa mesma rotina em outro campo:

``` html
<script type="text/javascript"> type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  /* para o input telefone */
  $("input[name='telefone']").focus(function(){
    if( $( this ).val()=='Digite seu telefone' )
    $( this ).val( '' );
  });
  $("input[name='telefone']").blur(function(){
    if( $( this ).val() == '' )
      $( this ).val( 'Digite seu telefone' );
  });
  /* para o input email */
  $("input[name='email']").focus(function(){
    if( $( this ).val()=='Digite seu e-mail' )
    $( this ).val( '' );
  });
  $("input[name='email']").blur(function(){
    if( $( this ).val() == '' )
      $( this ).val( 'Digite seu e-mail' );
  });
});
</script>

  <input type="text" name="telefone" value="Digite seu telefone" />
  <input type="text" name="email" value="Digite seu e-mail" />
```

Ou seja, tivemos que duplicar código !! O que é um absurdo, e devemos evitar fazer!

No próximo post, vamos ver como otimizar essa rotina, para então, melhorar ainda mais e evoluir para a criação do plugin.

Veja que primeiro identifiquei o problema, resolvi a situação, e só então incrementei e parti para &#8216;o nível avançado&#8217;.

[Parte 1](https://wbruno.com.br/jquery/criando-um-plugin-jquery-parte-1-comecando/)

[Parte 3](https://wbruno.com.br/jquery/criando-um-plugin-jquery-parte-3-otimizando/)
