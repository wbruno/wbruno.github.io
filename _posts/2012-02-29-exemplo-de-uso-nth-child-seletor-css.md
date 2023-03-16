---
id: 1808
title: Exemplo de uso do nth-child seletor css
date: 2012-02-29T15:19:00+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1808
permalink: /jquery/exemplo-de-uso-nth-child-seletor-css/
dsq_thread_id:
  - "2102324355"
categories:
  - jQuery
---
Selecionar o terceiro elemento de cada lista, para alterar alguma coisa do css dele.

Usar: .eq(3) é o mesmo que :nth-child(3), oq queremos é o **3n**

``` html
<html>
<head>
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js"></script>
<script type="text/javascript">
jQuery(document).ready(function(){
  jQuery('.lista li:nth-child(3n)').css('background','#f0f');
});
</script>
<style type="text/css">
.lista { width: 180px; }
.lista li {
  background: #f00;
  margin: 5px;
  width: 50px;
  height: 50px;
  float: left;
}
.clear { clear: both; }
</style>
</head>
<body>
  <h2 class="clear">Primeira lista</h2>
  <ul class="lista">
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
  </ul>
  <h2 class="clear">Segunda lista</h2>
  <ul class="lista">
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
  </ul>
  <h2 class="clear">Terceira lista</h2>
  <ul class="lista">
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
  </ul>
</body>
</html>
```