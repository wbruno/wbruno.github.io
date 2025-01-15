---
id: 974
title: 'Votação com estrelas [ star rating ] - Ajax jQuery'
date: 2011-05-20T07:00:13+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=974
permalink: /ajax/votacao-estrelas-star-rating-ajax-jquery/
dsq_thread_id:
  - "2101217564"
categories:
  - AJAX
---
Não vou explicar muito detalhadamente o HTML e CSS, pois está tudo bem simples.

Apenas para dar um contexto, usei alguns produtos, e embaixo de cada um deles, existem 5 estrelas cinza.

[<img src="/wp-content/uploads/2011/05/votacao.jpg" alt="" title="votacao" width="433" height="373" class="aligncenter size-full wp-image-975" srcset="/wp-content/uploads/2011/05/votacao.jpg 433w, /wp-content/uploads/2011/05/votacao-300x258.jpg 300w" sizes="(max-width: 433px) 100vw, 433px" />](/wp-content/uploads/2011/05/votacao.jpg)

<!--more-->



O comportamento será o seguinte:

> _Ao clicar em alguma estrela, ela e as anteriores a ela, deverão &#8216;acender'(ficar de outra cor). Clicando novamente, na última estrela escolhida, a pontuação será zerada, tornando todas as estrelas cinzas._

E além disso:

> _Se já estiver registrada alguma pontuação, ao clicar em uma estrela de menor valor, as estrelas &#8216;ativas&#8217; depois dessa, devem ser &#8216;desmarcadas&#8217;._

Okay, conforme prometi, o HTML+CSS, é mínimo e simples:

``` html
<html>
<head>
<style type="text/css">
* { margin: 0; padding: 0; list-style: none; }
.stars {
  width: 100px;
  height: 20px;
  margin: 5px auto 0 auto;
}
#produtos .stars li {
  background: url('star_groups.jpg') no-repeat;
  display: block;
  height: 20px;
  width: 20px;
  cursor: pointer;
  float: left;
}
#produtos .stars li.active {
  background-position: left -45px;
}
#produtos {
  width: 450px;
  margin: 20px auto 0 auto;
}
#produtos li {
  float: left;
  width: 150px;
  height: 200px;
  color: #1B57A3;
  text-align: center;
}
#produtos p {
  text-decoration: underline;
  font: 12px Arial, Verdana, sans-serif;
}
#sql {
  font: bold 20px Arial;
  color: #f00;
  text-align: center;
  clear: both;
}
</style>

</head>
<body>
  <ul id="produtos">
    <li>
      <img src="MacBook.jpg" alt="" />
      <p>MacBook</p>
      <ol class="stars"><li></li><li></li><li></li><li></li><li></li></ol>
      <input type="hidden" name="id_produto[]" value="15" />
    </li>
    <li>
      <img src="iMac.jpg" alt="" />
      <p>iMac</p>
      <ol class="stars"><li></li><li></li><li></li><li></li><li></li></ol>
      <input type="hidden" name="id_produto[]" value="12" />
    </li>
    <li>
      <img src="iPhone.jpg" alt="" />
      <p>iPhone</p>
      <ol class="stars"><li></li><li></li><li></li><li></li><li></li></ol>
      <input type="hidden" name="id_produto[]" value="5" />
    </li>

    <li>
      <img src="iPod_Nano.jpg" alt="" />
      <p>iPod Nano</p>
      <ol class="stars"><li></li><li></li><li></li><li></li><li></li></ol>
      <input type="hidden" name="id_produto[]" value="7" />
    </li>
    <li>
      <img src="iPod_Classic.jpg" alt="" />
      <p>iPod Classic</p>
      <ol class="stars"><li></li><li></li><li></li><li></li><li></li></ol>
      <input type="hidden" name="id_produto[]" value="9" />
    </li>
    <li>
      <img src="HP_LP3065.jpg" alt="" />
      <p>HP_LP3065</p>
      <ol class="stars"><li></li><li></li><li></li><li></li><li></li></ol>
      <input type="hidden" name="id_produto[]" value="22" />
    </li>
  </ul><!-- /produtos -->

  <div id="sql"></div>
</body>
</html>
```

Optei por deixar cada estrela como um LI, filho da Lista Ordenada **.stars**, pela simplicidade da marcação, e do javascript que vamos desenvolver.

Além disso, usei um input hidden dentro do container de cada produto, para sabermos qual o ID daquele produto no nosso banco de dados.

``` html
<script type="text/javascript"> type="text/javascript" src="http://code.jquery.com/jquery-1.6.1.min.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  $('.stars li').click(function(){
    var $this = $( this );
    var ol = $this.parent('ol');
    var rating = $this.index()+1;
    var id_produto = ol.parent('li').find("input[name='id_produto[]']").val();


    if( $this.hasClass('active') && !$this.next('li').hasClass('active') ){
      $( ol ).find('li').removeClass('active');
      rating = 0;
    }
    else{
      $( ol ).find('li').removeClass('active');
      for( var i=0; i<rating; i++ ){
        $( ol ).find('li').eq( i ).addClass('active');
      };
    }

    $.ajax({
      type: "POST",
      url: "retorno-votacao.php",
      data: "id_produto="+id_produto+"&voto="+rating,
      success: function( data ){
        $('#sql').html( data );
      }
    });
  });
});
</script>
```

O script server-side, é a parte mais simples:

``` php
<?php

if( $_SERVER['REQUEST_METHOD']=='POST' ){
  $id_produto = (int)getPost('id_produto');
  $voto = (int)getPost('voto');

  $sql = "INSERT INTO voto (`id_produto`, `voto`, `ip`, `data`) VALUES ( {$id_produto}, {$voto}, '{$_SERVER['REMOTE_ADDR']}', NOW() )";
  echo $sql;
}


function getPost( $key ){
  return isset( $_POST[ $key ] ) ? filter( $_POST[ $key ] ) : null;
}
function filter( $str ){
  return addslashes( $str );//a cargo do leitor
}
```

Veja que faço o INSERT na tabela \`voto\` a cada requisição que recebo.

Nesse ponto, as tuas regras de negócio devem ditar o tratamento que deve ser feito. Se cada cliente só pode votar uma vez em cada produto, se ele pode mudar o voto dele..

## <a href="http://www.wbruno.com.br/scripts/votacao-estrelas.php" target="_blank">Demonstração Online</a>
