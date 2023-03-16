---
id: 47
title: só ativar links ao carregar imagens
date: 2010-06-11T17:54:28+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=47
permalink: /javascript-puro/so-ativar-links-ao-carregar-imagens/
categories:
  - Javascript
---
Código simples e rápido que desativa os links do documento, e só os reativa, qndo as imagens estiverem completamente carregadas.

``` html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
        <title>Desativar Link antes do carregamento</title>
        <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />

<script type="text/javascript">
window.onload = function()
{
        var as = document.getElementsByTagName('a');
        for( var i=0; i<as.length; i++ )
        {
                as[i].onclick = function()
                {
                        return true;
                }
        }
}
</script>
<style type="text/css">

</style>
</head>
<body>

        <a href="teste.html"><img src="http://diogoparker.files.wordpress.com/2008/11/13-daylight_planet_wallpaper_by_janedoe873.jpg" alt="" /></a>
        <a href="teste.html"><img src="http://wallpaperslindos.files.wordpress.com/2008/12/outono_wallpaper_by_black_energy.jpg" alt="" /></a>
        <a href="teste.html"><img src="http://fc05.deviantart.com/fs20/f/2007/270/3/4/Balance_Wallpaper_by_nxxos.jpg" alt="" /></a>
        <script type="text/javascript">
        var as = document.getElementsByTagName('a');
        for( var i=0; i<as.length; i++ )
        {
                as[i].onclick = function()
                {
                        return false;
                }
        }
        </script>
</body>
</html>
```



ou seja, o script antes do fechamento do , após todo o HTML, será executado assim que o navegador terminar de ler todo o conteudo em texto, e o script no , condicionado ao window.onload, só rodará qndo o documento tiver completamente carregado. Testa ai