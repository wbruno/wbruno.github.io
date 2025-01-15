---
id: 1375
title: 'Simulando um mousestop() com jQuery - javascript'
date: 2011-09-03T10:14:51+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1375
permalink: /jquery/simulando-um-mousestop-jquery-javascript/
categories:
  - jQuery
---
Post rápido, para deixar registrado o código

<!--more-->

&nbsp;

``` html
<html>
<head>
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js"></script>
<script type="text/javascript">
var move = false;
var $box = null;
jQuery(document).ready(function(){
  $box = jQuery('.box').not('.active');

  $box.mousemove(function( e ){
    e.stopPropagation();
  });
  $box.mouseenter(function(){
    var $this = jQuery( this );
    $this.addClass('active');
  });
  $box.mouseleave(function(){
    var $this = jQuery( this );
    $this.removeClass('active');
  });

  jQuery(document).mousemove(function(){
    $box = jQuery('.box').not('.active');

    window.clearTimeout( stop );
    $box.stop(true, true).fadeIn( 700 );

    stop = window.setTimeout(function(){
      mousestop();
    }, 500 );
  });
  window.setTimeout(function(){
    $box.fadeOut( 2000 );
  }, 500);
});
function mousestop(){
  jQuery('.active').append('parou');
  jQuery('.box').not('.active').stop(true, true).fadeOut( 2000 );
}
</script>
<style type="text/css">
.box {
  background: #f0f;
  width: 70px;
  height: 70px;
  float: left;
  margin: 20px;
  text-align: center;
  color: #fff;
  font: 14px/65px Tahoma, sans-serif;

  position: absolute;
}
#box1 { top: 30px; left: 0px; }
#box2 { top: 70px; left: 150px; }
#box3 { top: 150px; left: 20px; }
#box4 { top: 0px; left: 220px; }
#box5 { top: 150px; left: 300px; }

</style>
</head>
<body>
  <div class="box" id="box1">
    Box 1
  </div><!-- /box -->
  <div class="box" id="box2">
    Box 2
  </div><!-- /box -->
  <div class="box" id="box3">
    Box 3
  </div><!-- /box -->
  <div class="box" id="box4">
    Box 4
  </div><!-- /box -->
  <div class="box" id="box5">
    Box 5
  </div><!-- /box -->
</body>
</html>
```

Dica: mecha o mouse, e deixe o mouse parado por um tempo.

Depois fique com o mouse sobre algum box, movimente dentro do box, e fique parado dentro dele.

## <a href="http://wbruno.com.br/scripts/mousestop.html" target="_blank">Demonstração</a>
