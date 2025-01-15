---
id: 1192
title: Brincando de random(), luta tira life RPG
date: 2011-07-15T01:03:21+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1192
permalink: /php/brincando-de-random-luta-tira-life-rpg/
categories:
  - PHP
---
^^ brincando um pouco aqui.

Fingindo que a &#8216;luta está acontecendo&#8217;. Na verdade a luta já está toda no html(o php processou), mas só vou mostrando aos poucos com javascript.

<!--more-->

## <a href="/scripts/rpg.php" target="_blank">Demonstração</a>

``` html
<html>
<head>
<script type="text/javascript">
function id( el ){
  return document.getElementById( el )
}
function changeDisplay( els, val ){
  for( var i=0; i<els.length; i++ ){
    els[ i ].style.display = val;
  }
}
function mostra( ps ){
  //alert( ps.length+' '+i );
  if( ps.length>i ) ps[i].style.display = 'block';
  else window.clearInterval( intv );
  i++;
}
// i e intv tem escopo global
var i = 0;
var intv = 0;
window.onload = function(){
  var ps = id('luta').getElementsByTagName('p');
  changeDisplay( ps, 'none' );

  intv = window.setInterval( mostra, 1000, ps );
}
</script>
<style type="text/css">
* { margin: 0; padding: 0; }
</style>
</head>
<body>
<div id="luta">
<?php
  $life1 = 100;
  $life2 = 100;
  while( $life1>0 && $life2>0 )
  {
    /* você */
    $hit = rand( 5,30 );
    if( $hit > $life1 ) $hit = $life1;//não deixar receber mais dano do o life

    $life1 -= $hit;
    echo '<p>Você recebeu '.$hit.' de dano, agora seu life é: '.$life1.'</p>';

    /* adversário */
    $hit2 = rand( 5,30 );
    if( $hit2 > $life2 ) $hit2 = $life2;//não deixar receber mais dano do o life

    $life2 -= $hit2;
    echo '<p>Seu adversário recebeu '.$hit2.' de dano, agora o life dele é: '.$life2.'</p><br />';
  }
  if( $life1>$life2 ) echo '<p>Parabéns, você ganhou!</p>';
  else if( $life1<$life2 ) echo '<p>Azar, seu adversário ganhou</p>';
  else echo '<p>Empate!</p>';
?>
</div><!-- /luta -->
</body>
</html>
```

=) qq coisa comentem
