---
id: 1038
title: Navegação sem refresh – carregando conteúdo com ajax em div 2
date: 2011-05-27T07:00:13+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=1038
permalink: '/ajax/navegacao-sem-refresh-%e2%80%93-carregando-conteudo-ajax-em-div-2/'
dsq_thread_id:
  - "2100751624"
categories:
  - AJAX
tags:
  - navegação
---
Eu já havia postado essa solução: <http://wbruno.com.br/ajax/navegacao-sem-refresh-carregando-conteudo-ajax-em-div/>.

Porém, ai a galera começa a querer um &#8216;efeito de fade&#8217;, &#8216;um gif de carregando..&#8217;.

E para resolve isso, é melhor que descartemos a função **.load()** do jQuery, para usarmos uma em que temos mais controle do que está ocorrendo.

<!--more-->



Nesse caso, vou optar pelo **$.ajax**, já que **$.get** e **$.post**, são apenas atalhos para ela.

A maior alteração, será nesse trecho do script anterior:

``` js
$("#content").load( href +" #content");
```

Vamos fazer algo mais sofisticado.

``` html
<html>
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />

  <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.6.1/jquery.min.js"></script>
  <script type="text/javascript">
  $(document).ready(function(){
    var content = $('#content');

    //pre carregando o gif
    loading = new Image(); loading.src = 'loading.gif';
    $('#menu a').live('click', function( e ){
      e.preventDefault();
      content.html( '<img src="loading.gif" />' );

      var href = $( this ).attr('href');
      $.ajax({
        url: href,
        success: function( response ){
          //forçando o parser
          var data = $( '<div>'+response+'</div>' ).find('#content').html();

          //apenas atrasando a troca, para mostrarmos o loading
          window.setTimeout( function(){
            content.fadeOut('slow', function(){
              content.html( data ).fadeIn();
            });
          }, 500 );
        }
      });

    });
  });
  </script>
</head>
<body>
  <ul id="menu">
    <li><a href="index.html">Home</a></li>
    <li><a href="fotos.html">Fotos</a></li>
    <li><a href="contato.html">Contato</a></li>
  </ul><!-- /menu -->
  <div id="content">
    <h1>Bem Vindo!</h1>
    <p>Essa eh a home desse nome pseudo-site.</p>
  </div><!-- /content -->
</body>
</html>
```

Apenas lembrando que as páginas internas, devem continuar com o código HTML completo, pois queremos que nosso site continue funcionando caso não haja suporte a javascript no navegador do usuário.

``` html
<html>
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
</head>
<body>
  <ul id="menu">
    <li><a href="index.html">Home</a></li>
    <li><a href="fotos.html">Fotos</a></li>
    <li><a href="contato.html">Contato</a></li>
  </ul><!-- /menu -->
  <div id="content">
    <h1>Fotos</h1>


    Fotos fotos fotos
  </div><!-- /content -->
</body>
</html>
```

## <a href="http://wbruno.com.br/scripts/ajaxdiv.html" target="_blank">Demonstração</a>

## Se vc já usou esse script

E **teve problemas** com os outros scripts do seu site, veja estes links:

[Usando lightbox em página carregada com ajax](http://wbruno.com.br/2011/08/22/usando-lightbox-em-pagina-carregada-ajax/)

[Carregando conteudo com ajax, trocando a URL com jQuery](http://wbruno.com.br/2011/11/25/carregando-conteudo-ajax-trocando-url-jquery/)

[O método .live() do jQuery](http://wbruno.com.br/2011/03/18/metodo-live-jquery/)

[Como debugar JavaScript com o Firefox ? – erros comuns](http://wbruno.com.br/2011/03/31/como-debugar-javascript-firefox-erros-comuns/)
