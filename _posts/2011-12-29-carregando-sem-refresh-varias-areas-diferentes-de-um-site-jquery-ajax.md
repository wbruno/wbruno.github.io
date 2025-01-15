---
id: 1663
title: 'Carregando sem refresh, várias áreas diferentes de um site - jQuery.ajax'
date: 2011-12-29T10:55:46+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1663
permalink: /ajax/carregando-sem-refresh-varias-areas-diferentes-de-um-site-jquery-ajax/
dsq_thread_id:
  - "2102321307"
categories:
  - AJAX
---
Eu já postei aqui no meu blog, como <a href="https://wbruno.com.br/ajax/navegacao-sem-refresh-carregando-conteudo-ajax-em-div/" target="_blank">carregar conteudo com ajax em div</a>, daí, aprimorei aquele código, e mostrei como <a href="https://wbruno.com.br/ajax/navegacao-sem-refresh-carregando-conteudo-ajax-em-div/" target="_blank">carregar conteudo com ajax, colocando também um gif de loading</a>.. e também como fazer tudo isso de cima, ainda <a href="https://wbruno.com.br/ajax/carregando-conteudo-ajax-trocando-url-jquery/" target="_blank">trocando a URL, e usando um plugin na página interna</a>.

Hoje é dia de carregar várias divs &#8216;separadas&#8217;, várias áreas diferentes com ajax.

<!--more-->



Já vi no fórum um cara(com dúvida) resolvendo isso, de uma forma &#8216;natural&#8217; do ponto de vista de pensamento humano, mas terrível para performance e manutenção do site.

O código que ele usou era mais ou menos assim:

``` js
jQuery(document).ready(function(){
  var sidebar = jQuery('#sidebar');
  var content = jQuery('#content');
  var other = jQuery('#other');

  jQuery('#menu a').click(function( e ){
    e.preventDefault();
    if( jQuery( this ).attr('href')=='home.html' )
    {
      sidebar.load('home_sidebar.html');
      content.load('home_content.html');
      other.load('home_other.html');
    }
    else if( jQuery( this ).attr('href')=='cadastro.html' )
    {
      sidebar.load('cadastro_sidebar.html');
      content.load('cadastro_content.html');
      other.load('cadastro_other.html');
    }
  });
});
```

Ou seja, a cada clique em um link do menu, ele fazia 3 requests. Um para cada &#8216;área&#8217; do site.

Tinha que manter 3 arquivos distintos para cada link, e esse jogo de if/else para saber quais arquivos ele deve invocar.

> Isso deve ter um &#8216;mau cheiro&#8217;.

A cada clique fazer 3 requisições, e ter que manter 3 arquivos separados para cada área.. além de que o site &#8216;não vai funcionar corretamente&#8217;, se o suporte a js estiver desabilitado&#8230; muitos motivos para evidenciar que algo está errado.

> Mas então, o que podemos fazer?

A minha sugestão, é aproveitar o ótimo parser de HTML da lib jQuery, fazer um único request, e então direcionar cada conteúdo para o local específico.

``` html
<html>
<head>
<script type="text/javascript" src="jquery.min.js"></script>
<script type="text/javascript">
jQuery(document).ready(function(){
  var sidebar = jQuery('#sidebar');
  var content = jQuery('#content');
  var other = jQuery('#other');

  request( 'home.html' );

  function m_load( data )
  {
    var text = jQuery( '<div>'+data+'</div>' );//forçando o parser

    sidebar.html( text.find('#sidebar').html() );
    content.html( text.find('#content').html() );
    other.html( text.find('#other').html() );

    jQuery(document).attr( 'title', text.find('title').html() );
  }
  function request( file )
  {
    jQuery.ajax({
      url: file,
      success: function( data )
      {
        m_load( data );
      }
    });
  }
  jQuery('#menu a').click(function( e ){
    e.preventDefault();
    request( jQuery( this ).attr('href') );
  });
});

</script>
</head>
<body>
  <ul id="menu">
    <li><a href="home.html">Home</a></li>
    <li><a href="cadastro.html">Cadastro</a></li>
    <li><a href="contato.html">Contato</a></li>
  </ul><!-- /menu -->
  <div id="sidebar">

  </div><!-- /sidebar -->
  <div id="content">

  </div><!-- /content -->
  <div id="other">

  </div><!-- /other -->
</body>
</html>
```

Note que além de fazer o parser do retorno:

``` js
var text = jQuery( '<div>'+data+'</div>' );//forçando o parser

    sidebar.html( text.find('#sidebar').html() );
    content.html( text.find('#content').html() );
    other.html( text.find('#other').html() );
```

eu também faço a troca do title do documento:

``` js
jQuery(document).attr( 'title', text.find('title').html() );
```

## [Demonstração](http://wbruno.com.br/scripts/index_3areas.html)

Se vc tiver o firebug instalado, confira na aba Net|Rede -> xhr que faço apenas uma requisição.
