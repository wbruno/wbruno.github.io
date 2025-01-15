---
id: 1613
title: Slideshow JavaScript com botões de comando(play,stop,prev e next) usando o jQuery.Cycle
date: 2011-11-24T00:47:12+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1613
permalink: /jquery/slideshow-javascript-botoes-de-comandoplaystopprev-next-usando-jquery-cycle/
dsq_thread_id:
  - "2100808187"
categories:
  - jQuery
tags:
  - plugin
  - slideshow
---
Coisa rápida&#8230; nosso velho e conhecido slideshow.

Porém, denovo, apenas para deixar registrado aqui, a flexibilidade de uso do plugin jQuery.Cycle, e a facilidade de implementação.

<!--more-->

``` html
<html>
<head>
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.0/jquery.min.js"></script>
<script type="text/javascript" src="js/jquery.cycle-2.97.all.min.js"></script>
<script type="text/javascript">
jQuery(document).ready(function(){
  jQuery('#slideshow2').cycle({
    fx: 'fade',
    next: '#proxima',
    prev: '#anterior'
  });
  jQuery('#pausa').click(function(){
    $('#slideshow2').cycle('pause');
  });
  jQuery('#play').click(function(){
    $('#slideshow2').cycle('resume');
  });
});
</script>
<style type="text/css">
* {
  margin: 0; padding: 0; border: none;
}
body { font: 12px Arial; }
#slideshow2 {
  list-style: none;
  height: 185px;
  width: 220px;
  overflow: hidden;
}
#slideshow2 li {
  height: 100%;
}
#slideshow2 p {
  font-weight: bold;
  font-size: 13px;
}
#ctrls img { cursor: pointer; }
</style>
</head>
<body>
  <ul id="slideshow2">
    <li>
      <a href="?noticia=2660/nivel-de-estoques-de-aco-e-positivo--mas-perspectiva-e-de-queda-dos-precos-do-setor">
        <img src="uploads/20111123-213901.jpg" alt="Metalurgia e Distribuição" />
      </a>
      <p>Nível de estoques de aço é positivo, mas perspectiva é de queda d...</p>
    </li>
    <li>
      <a href="?noticia=2660/nivel-de-estoques-de-aco-e-positivo--mas-perspectiva-e-de-queda-dos-precos-do-setor">
        <img src="uploads/20111123-213612.jpg" alt="Metalurgia e Distribuição" />
      </a>
      <p>Inscrições para concurso da Petrobras começam nesta quinta salári...</p>
    </li>
    <li>
      <a href="?noticia=2660/nivel-de-estoques-de-aco-e-positivo--mas-perspectiva-e-de-queda-dos-precos-do-setor">
        <img src="uploads/20111122-230224.jpg" alt="Metalurgia e Distribuição" />
      </a>
      <p>Engenheiro norte-americano cria moto elétrica com uma roda só</p>
    </li>
  </ul><!-- /slideshow2 -->

  <div id="ctrls">
    <img src="img/slide_anterior.gif" width="76px" height="20px" alt="anterior" id="anterior" />
    <img src="img/slide_play.gif" width="23px" height="20px" alt="play" id="play" />
    <img src="img/slide_pausa.gif" width="23px" height="20px" alt="pausa" id="pausa" />
    <img src="img/slide_proxima.gif" width="73px" height="20px" alt="proxima" id="proxima" />
  </div><!-- /ctrls -->
</body>
</html>
```

É isso ai. Comentem!

## [Demonstração](/scripts/slide-ctrls.html)
