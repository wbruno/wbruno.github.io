---
id: 343
title: 'Criando um plugin jQuery - parte 3 - Otimizando'
date: 2011-03-26T07:00:50+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=343
permalink: /jquery/criando-um-plugin-jquery-parte-3-otimizando/
dsq_thread_id:
  - "2105270277"
categories:
  - jQuery
tags:
  - plugin
---
Salve salve galera!

Se vc está acompanhando essa série de posts até aqui, então estamos indo bem.

Evoluindo em cada passo. Poderíamos parar na parte 2, e deixar apenas aquilo, mas não estou contente com aquele código, pq se forem 2 inputs, tenho 2 vezes o mesmo código, mas e se forem 5 ou 10 inputs ?

Inimaginável mantermos um código assim. Legal, aprendemos a resolver o problema, então agora, vamos aprender a como melhorar nossa solução.

A primeira resposta óbvia que deveria vir a nossa mente, é: criar uma **function** reaproveitável !

<!--more-->

Partindo dessa premissa, nossa function, precisa de 2 parâmetros [ pois são somente duas coisas que variam ]

``` js
function limpa( el, msg ){}
```

ou seja, o elemento e a mensagem. Afinal, é somente isso que muda e precisa mudar.

Fica fácil de observarmos isso, olhando a duplicação que fizemos na parte 2, para ter mais de um input.

Visto isso, chegamos no seguinte:

``` js
function limpa( el, msg )
{
  el.focus(function(){
    if( $( this ).val()==msg )
      $( this ).val( '' );
  });
  el.blur(function(){
    if( $( this ).val() == '' )
      $( this ).val( msg );
  });
}
```

Legal, e a chamada fica apenas:

``` js
$(document).ready(function(){
  limpa( $("input[name='telefone']"), 'Digite seu telefone' );
  limpa( $("input[name='email']"), 'Digite seu e-mail' );
});
```

beeem melhor do que anteriormente, e agora para novos inputs, só precisamos chamar a função novamente, informando para quais campos ela deve agir, e qual era a mensagem default.

Só que como prometi, vamos transformar isso em um plugin, apenas pela brincadeira de fazer um.

<a href="http://docs.jquery.com/Plugins/Authoring" target="_blank">http://docs.jquery.com/Plugins/Authoring</a>

``` html
<html>
<head>
  <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js"></script>
  <script type="text/javascript">
  /**
   * @file jquery.placeholder.js
   * @author William Moraes - wbruno
   * @site http://wbruno.com.br
   * @version 1.0 beta
   */

  function trim( str ){ return str.replace(/^\s+|\s+$/g,""); }

  jQuery.fn.limpa = function( settings ){
    var $this = jQuery( this );
    var defaults = {
      msg: $this.val(),
      default: 'defaultInput',
      active: 'activeInput'
    }
    settings = jQuery.extend(defaults, settings);

    $this.focus(function(){
      if( $this.val()==settings.msg )
        $this.removeClass( settings.default ).addClass( settings.active ).val( '' );
    });
    $this.blur(function(){
      if( trim( $this.val() ) == '' )
        $this.removeClass( settings.active ).addClass( settings.default ).val( settings.msg );
    });
    if( $this.val()==settings.msg ) $this.addClass( settings.default );

    return $this;
  }
  $(document).ready(function(){
    $("input[name='telefone']").limpa();
    $("input[name='email']").limpa();
    $("input[name='cep']").limpa();
  });
  </script>
  <style type="text/css">
  .defaultInput { color: #b9b3d0; }
  .activeInput { color: #000; }
  </style>
</head>
<body>
  <input type="text" name="telefone" value="Digite seu telefone" />
  <input type="text" name="email" value="Digite seu e-mail" />
  <input type="text" name="cep" value="Digite seu cep" />
</body>
</html>
```

Adicionei uma &#8216;perfumaria&#8217; a mais, trocar a class, caso a mensagem esteja default.

Para o nosso escopo inicial, nem era necessário as configurações default ali, como a mensagem e tal, eu poderia ter usado direto:

``` js
jQuery.fn.limpa = function( settings ){
    var $this = jQuery( this );
    var msg = $this.val();

    $this.focus(function(){
      if( $this.val()==msg )
        $this.val( '' );
    });
    $this.blur(function(){
      if( $this.val() == '' )
        $this.val( msg );
    });

    return $this;
  }
```

ai o plugin ficaria ridicularmente simples, e apenas resolveria o mesmo que a nossa function.

Se vc se perdeu na versão &#8216;completa&#8217;, olhe esta ultima que postei, entenda, e depois veja a outra novamente.

Bom, é isso. Acredito que consegui explicar bem oque pretendia.

Caso surjam duvidas quanto ao plugin, utilização dele, ou o motivo de eu ter usado as classes css, e deixar a mensagem default configurável, eu posso explicar depois.

Obrigado por ter acompanhando esses 3 posts. Espero que eles sejam úteis, para lhe ajudar a pensar sobre &#8216;como programar&#8217;, e não apenas esse código em especifico que postei.

## <a href="http://www.wbruno.com.br/placeholder/" target="_blank">Demonstração</a>

[Parte 1](https://wbruno.com.br/jquery/criando-um-plugin-jquery-parte-1-comecando/)

[Parte 2](https://wbruno.com.br/jquery/criando-um-plugin-jquery-parte-2-codificando/)
