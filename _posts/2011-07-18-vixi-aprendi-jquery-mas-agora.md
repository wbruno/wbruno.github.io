---
id: 1117
title: 'Vixi! &#8216;aprendi&#8217; jQuery mas e agora ?'
date: 2011-07-18T07:00:16+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1117
permalink: /jquery/vixi-aprendi-jquery-mas-agora/
dsq_thread_id:
  - "2100963314"
categories:
  - jQuery
---
Hum.. eu já havia dito que na minha opinião, o fluxo correto, é <a href="https://wbruno.com.br/opiniao/nao-jquery-nao-aprenda-qualquer-framework-antes-de/" target="_blank">primeiro aprender javascript, para só depois estudar a biblioteca</a>.

Mas e se você já está no meio do caminho ?

Achava javaScript &#8216;muito dificil&#8217;, chato, não via nem utilidade.. e então foi para o mundo do &#8220;Write Less, Do More&#8221;, sem ter uma boa base em js..

<!--more-->

Bom, ai dependendo do tempo e experiência que vc tem em programação, vc pode saber oque está fazendo, ou não.

Enfim, gostaria de listar algumas coisas interessantes sobre a biblioteca, mas que pelo menos eu, nunca vi sendo discutido por ai.

## jQuery é apenas javascript

Isso e nada mais. Se fizeram com a lib, dá para fazer sem. E o mesmo se aplica, qndo precisamos pensar, que a estrutura da sintaxe do jQuery, é apenas javascript.

Vamos olhar por partes:

``` js
$(document)```

Estamos invocando **uma função**, chamada $, passando o objeto global <u>document</u> para ela. Nada de mais.

``` js
.ready()```

Agora conseguimos usar um método apartir da função anterior, pq jQuery, foi escrito com base em no pattern **Fluent Interface**. O método ready(), aguarda que o DOM esteja pronto. E isso acontece **antes** do evento window.onload, pois o window.onload espera também que as imagens estejam todas carregadas. Enqnto o .ready() aguarda apenas a marcação html.

## Funções anônimas

Okay, continuando temos sempre um:

``` js
function(){

}
```

Poxa! e oque é isso ? é apenas uma function, só que _sem nome_ certo ?

estamos acostumados com funções assim:

``` js
function a(){}
```

, sendo então **a**, o _nome_ da nossa função.

Blz, então passamos uma **função anônima**, para o callback do método .ready()!

caramba! qnta coisa que fazíamos sem notar, ne?!

Hum.. e qual o ponto interessante disso ? é que devemos poder fazer:

``` js
var a = function(){
    alert( 'ae' );
  };
  $(document).ready( a );
```

que pelo menos tecnicamente, deve funcionar, certo ?

Certíssimo! e funciona. Deu na mesma, se tivessemos feito:

``` js
$(document).ready(function(){
    alert( 'ae' );
  });
```

Não estou roubando, se fosse um plugin:

``` js
var a = function(){
    $('a[rel*=facebox]').facebox({
      loadingImage : 'src/loading.gif',
      closeImage   : 'src/closelabel.png'
    });
  };
  $(document).ready( a );
```

também continuaria funcionando. Tudo normal.

## jSON

Mas olha que interessante agora, o plugin recebe como parâmetro um objeto javascript.

Só que estamos jogando esse objeto diretamente ali. Se por algum motivo tivermos que instanciar novamente o mesmo plugin, já vi códigos assim:

``` js
$('a[rel*=facebox]').facebox({
      loadingImage : 'src/loading.gif',
      closeImage   : 'src/closelabel.png'
    });
    $('a#tal').facebox({
      loadingImage : 'src/loading.gif',
      closeImage   : 'src/closelabel.png'
    });
```

hum&#8230; deve ser evidente a duplicação de instruções.

E oque devemos fazer com isso ?

Juntar em uma só!

se não pudermos fazer:

``` js
$('a[rel*=facebox], a#tal').facebox(```

por qq motivo, seja falta de suporte a arrays de objetos do plugin, ou escopos diferentes, sei lá&#8230; podemos dar um nome para esse nosso jSON de configuração, e então enviar ele:

``` js
var configs = {
      loadingImage : 'src/loading.gif',
      closeImage   : 'src/closelabel.png'
    };
  $(document).ready(function(){
    $('a[rel*=facebox]').facebox( configs );
    $('a#tal').facebox( configs );
  });
```

a beleza disso, é que tudo funciona como deveria, afinal estamos falando de javascript, e a estrutura da linguagem permite essas coisas.

Agora colocando tudode uma vez:

``` js
var configs = {
      loadingImage : 'src/loading.gif',
      closeImage   : 'src/closelabel.png'
    };
  var a = function(){
    $('a[rel*=facebox]').facebox( configs );
    $('a#tal').facebox( configs );
  };
  $(document).ready( a );
```

deve estar meio estranho, ou até ilegível, já que não estamos acostumados com isso, porém, é normal a forma com que escrevi, e é exatamente isso que fazemos todos os dias.

Só que sem notar. E esse é o problema. Somos mais fortes e programaremos melhor, qndo entendermos cada detalhe do que fizermos.

## noConflict()?

Hum&#8230; essa é interessante:

``` js
(function( $ ){
    $(document).ready(function(){
      alert('ae');
    });
  })(jQuery);
```

E ai? que diabos é isso ?

é uma função anônima autoexecutável, que recebe o objeto **jQuery** como parâmetro.

Veja que o argumento é $, então podemos usar esse símbolo normalmente dentro dessa function, sem nos preocupar com conflito, pois externamente a essa function, passamos um **jQuery**, e o $, ficou restrito ao escopo dessa anônima.

**clousures** é um conceito muito interessante. Vale a pena pesquisar e entender a beleza.

## Pra quê?

Lógico que vc não precisa se lembrar de tudo oque eu disse, cada vez que for escrever algo com jQuery. Mas é melhor saber oque está usando, do apenas usar sem saber, ne?! =)
