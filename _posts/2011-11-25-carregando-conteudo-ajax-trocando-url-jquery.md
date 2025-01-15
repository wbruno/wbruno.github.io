---
id: 1623
title: Carregando conteudo com ajax, trocando a URL com jQuery
date: 2011-11-25T15:53:39+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1623
permalink: /ajax/carregando-conteudo-ajax-trocando-url-jquery/
dsq_thread_id:
  - "2100793219"
categories:
  - AJAX
tags:
  - lightbox
---
Vamos lá.. esse post é mais ou menos uma mescla de outros 3 posts meus.

Nesse script eu vou, carregar conteudo com ajax(usando jQuery), vou deixar o lightbox funcionando, e também fazer com que a URL mude.

Para que o visitante possa dar F5, e o conteudo &#8220;continuar lá&#8221;(sem voltar para a index). E também, para que ele consiga sei lá, enviar para um amigo, uma página interna do seu site.

<!--more-->



Bom, o código javascript ficou assim:

``` js
$(document).ready(function(){
    var content = $('#content');

    //pre carregando o gif
    loading = new Image(); loading.src = 'ico-loading.gif';



    $('#menu a').click(function( e ){
      var arq = pega_arq( $( this ).attr('href') );
      abre( arq, content );
    });


    /* iniciando com a home */
    abre( pega_arq( document.location.href ), content );
  });
  function abre( href, content ){
    content.html( '<img src="ico-loading.gif" />' );


    $.ajax({
      url: href,
      success: function( response ){
        content.delay(1000).hide().html( response ).fadeIn();

        init_plugins( href );
      }
    });
  }
  function pega_arq( url ){
    var file = url.split('#');
    return ( file[1] ) ? file[1]+'.html' : 'home.html';
  }
  function init_plugins( href )
  {
    if( href=='lightbox.html' )
    {
      $('#gallery a').click(function( e ){
        e.preventDefault();
      })
      $('#gallery').lightBox();
    }
  }
```

## <a href="http://www.wbruno.com.br/scripts/ajax-url.html#lightbox" target="_blank">Usando lightbox em página que foi carregada com ajax</a>

É isso. Comentem! Sério.. se vc usar, deixa um comentário aqui..
