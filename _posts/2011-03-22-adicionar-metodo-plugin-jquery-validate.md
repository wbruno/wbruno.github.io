---
id: 295
title: Adicionar método no plugin jQuery.validate
date: 2011-03-22T09:46:24+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=295
permalink: /jquery/adicionar-metodo-plugin-jquery-validate/
dsq_thread_id:
  - "2100751093"
categories:
  - jQuery
tags:
  - plugin
---
Boas Galera !!

Passando por aqui apenas para compartilhar, um método adicional que desenvolvi para o plugin jQuery.validate.

<!--more-->

``` js
$(document).ready(function(){
  jQuery.validator.addMethod("notEquals", function(value, element, config){
    return value!=config;
  }, 'Digite um valor');
});
```

Bom.. olhando assim, para até complicado, mas com calma, dá para perceber que ele não faz nada além de retornar um booleano.

Para criar os teus próprios métodos, o melhor guia é a documentação:

<a href="http://docs.jquery.com/Plugins/Validation/Validator/addMethod#namemethodmessage" target="_blank">http://docs.jquery.com/Plugins/Validation/Validator/addMethod#namemethodmessage</a>

Lendo direitinho, e até vendo métodos de outras pessoas para exemplo e guia, vc vai longe.

Voltando, agora que adicionamos um método de validação ao plugin, basta usá-lo…

``` js
rules:{
    empresa: {
    required: true, notEquals: 'Empresa'},
```

E então a mensagem, caso o usuário não digite:

``` js
empresa: {
    required: "Digite o nome da sua empresa",
    notEquals: "Digite o nome da sua empresa!" },
```

Note o **notEquals**.

veja, ali no parâmetro, eu mando a string &#8216;Empresa&#8217;, para o campo input name=&#8221;empresa&#8221;.

Esse método me foi necessário e útil, pq meu formulário era assim:

[<img class="aligncenter size-full wp-image-296" title="Screen shot 2011-03-22 at 9.39.32 AM" src="/wp-content/uploads/2011/03/Screen-shot-2011-03-22-at-9.39.32-AM.png" alt="" width="343" height="125" srcset="/wp-content/uploads/2011/03/Screen-shot-2011-03-22-at-9.39.32-AM.png 343w, /wp-content/uploads/2011/03/Screen-shot-2011-03-22-at-9.39.32-AM-300x109.png 300w" sizes="(max-width: 343px) 100vw, 343px" />](/wp-content/uploads/2011/03/Screen-shot-2011-03-22-at-9.39.32-AM.png)

Desses que tem uma descrição do que vc quer que o usuário digite. Sem esse método que adicionei ao validate, a validação passaria direto, e enviaria a string &#8220;Empresa&#8221;, sem o usuário ter digitado nada.

Porém graças ao **notEquals**:

[<img class="aligncenter size-full wp-image-297" title="Screen shot 2011-03-22 at 9.41.30 AM" src="/wp-content/uploads/2011/03/Screen-shot-2011-03-22-at-9.41.30-AM.png" alt="" width="337" height="65" srcset="/wp-content/uploads/2011/03/Screen-shot-2011-03-22-at-9.41.30-AM.png 337w, /wp-content/uploads/2011/03/Screen-shot-2011-03-22-at-9.41.30-AM-300x57.png 300w" sizes="(max-width: 337px) 100vw, 337px" />](/wp-content/uploads/2011/03/Screen-shot-2011-03-22-at-9.41.30-AM.png)

Vale lembrar que para tal, eu precisei criar também uma [funçãozinha rápida para apagar o campo no evento onfocus](https://wbruno.com.br/jquery/criando-um-plugin-jquery-parte-1-comecando/).

É isso galera, comentem qualquer dúvida.
