---
id: 1579
title: Menu DropDown abrindo com click, e fechando ao clicar fora
date: 2011-10-26T22:55:29+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1579
permalink: /jquery/menu-dropdown-abrindo-click-fechando-ao-clicar-fora/
dsq_thread_id:
  - "2100718235"
categories:
  - jQuery
---
O nosso conhecido DropDown, porém abrindo com um click na LI, e fechando com um click &#8216;fora&#8217;.
  
<!--more-->

Note que esse clique fora, quer dizer clicar em tudo oque não seja o menu. Logo, o elemento que temos de cara para isso, é o **body**. Convém lembrar, que os eventos em javascript propagam de filho para pai.

Sendo assim, um click no menu, dispara também um click no body.
  
Por isso, que uso ali, o método **.stopPropagation()**, pois qndo eu clicar no #menu li(para abrir o sub especifico), não quero que seja disparado o click do body(que fecha os subs).

Bom, é isso, o código está simples e é auto explicativo.

``` html
<html>
<head>
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript">
jQuery(document).ready(function( $ ){
  var uls = $('#menu ul');
  uls.hide();

  $('#menu > li').click(function( e ){
    e.stopPropagation();
    uls.hide();
    $( this ).find('ul').show();
  });
  $('#menu ul').click(function( e ){
    e.stopPropagation();
  });
  $('body').click(function(){
    uls.hide();
  });
});
</script>
<style type="text/css">
* { list-style: none; }
html, body { height: 100%; }
body { font: 12px/12px Tahoma, sans-serif; color: #666; }
#main { min-height: 100%; }
#menu { height: 30px; }
#menu li {
  position: relative;
  float: left;
  padding: 0 10px;
  height: 30px;
  line-height: 30px;
  border: 1px solid #666;
}
#menu ul {
  position: absolute;
  top: 30px;
  left: -1px;
  border: 1px solid #666;
  background: #fff;
}
#menu li li {
  width: 200px;
  border: none;
}
</style>
</head>
<body>
<div id="main">
  <ul id="menu">
    <li>Abrir sub 1
      <ul>
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
        <li>Item 4</li>
      </ul>
    </li>
    <li>Abrir sub 2
      <ul>
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
      </ul>
    </li>  
  </ul><!-- /menu -->
</div><!-- /main -->
</body>
</html>
```

## [Demonstração](/scripts/menu-click.html)

é isso ai. Comente se te ajudou, ou se tiver alguma dúvida/sugestão.