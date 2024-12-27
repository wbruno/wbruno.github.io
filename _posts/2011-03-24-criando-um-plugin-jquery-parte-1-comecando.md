---
id: 334
title: 'Criando um plugin jQuery &#8211; parte 1 &#8211; Começando'
date: 2011-03-24T07:20:43+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=334
permalink: /jquery/criando-um-plugin-jquery-parte-1-comecando/
dsq_thread_id:
  - "2114855598"
categories:
  - jQuery
tags:
  - plugin
---
Bom.. vou &#8216;desenvolver&#8217; um plugin jQuery do começo. Apartir da idéia.

Sempre que vamos desenvolver um script, precisamos ter em mente, que qualquer script só tem sentido se ele for criado para &#8216;resolver um problema&#8217;, e então, tendo o &#8216;problema&#8217; bem definido, podemos encontrar formas de resolvê-lo.

**Problema:**

> _&#8220;Possuo campos input em um formulário, onde dentro deles existe uma descrição do que o usuario deve digitar ali.

> Gostaria que quando o usuário entrasse nesse campo(clicasse, tentasse preencher..), esse valor default fosse apagado.

> Porém, se o usuário sair deste campo, sem escrever nada, esse valor &#8216;default&#8217;, deve voltar a aparecer. Sendo que se ele preencher, fique lá o que ele digitou.&#8221;

>_

<!--more-->

Okay, problema bem definido podemos rascunhar.

Primeiro passo, é identificar os pontos importantes da mensagem. [Interpretação de Texto] !!

> _&#8220;Possuo campos input em um formulário&#8221;_

``` html
<input type="text" name="telefone" />
  <input type="text" name="email" />
```

Muito importante essa iniciativa! Faça um passo de cada vez, e não tenha medo de começar.

É lógico que se vc não tentar, não vai conseguir fazer, ou empacar, e nem produzir nada. É importante ter a iniciativa.

> _&#8220;onde dentro deles existe uma descrição do que o usuario deve digitar ali.&#8221;_

Isso significa, nada mais do que:

``` html
<input type="text" name="telefone" value="Digite seu telefone" />
  <input type="text" name="email" value="Digite seu e-mail" />
```

[<img src="/wp-content/uploads/2011/03/Screen-shot-2011-03-23-at-2.28.35-PM.png" alt="" title="Screen shot 2011-03-23 at 2.28.35 PM" width="330" height="35" class="aligncenter size-full wp-image-335" srcset="/wp-content/uploads/2011/03/Screen-shot-2011-03-23-at-2.28.35-PM.png 330w, /wp-content/uploads/2011/03/Screen-shot-2011-03-23-at-2.28.35-PM-300x31.png 300w" sizes="(max-width: 330px) 100vw, 330px" />](/wp-content/uploads/2011/03/Screen-shot-2011-03-23-at-2.28.35-PM.png)

Bacana. Começamos.

Eu poderia resolver isso sem jQuery (depois faço um post resolvendo essa situação só com js puro), porém como quero mostrar a evolução do pensamento(e não como desenvolver o código em si), vamos usar jQuery:

``` html
<script type="text/javascript"> type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js"></script>
<script type="text/javascript">
$(document).ready(function(){

});
</script>
```

Básico ne!? porém vejo muita gente, que nem faz isso, e já está se descabelando que &#8216;não sabe começar&#8217;.

Poxa, <u>começar</u>, é isso ai. Fiz o html, preparei a estrutura do jQuery.. pronto, comecei.

Não resolvi o problema ainda, mas já dei um belo passo para chegar lá.

Para não ficar muito extenso o texto, vou dividir esse meu pensamento em uma série pequena de posts.

[Parte 2](https://wbruno.com.br/jquery/criando-um-plugin-jquery-parte-2-codificando/)

[Parte 3](https://wbruno.com.br/jquery/criando-um-plugin-jquery-parte-3-otimizando/)
