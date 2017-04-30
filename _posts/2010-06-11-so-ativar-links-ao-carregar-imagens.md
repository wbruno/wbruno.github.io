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

<pre name="code" class="html">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"&gt;
&lt;html xmlns="http://www.w3.org/1999/xhtml"&gt;
&lt;head&gt;
        &lt;title&gt;Desativar Link antes do carregamento&lt;/title&gt;
        &lt;meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" /&gt;

&lt;script type="text/javascript"&gt;
window.onload = function()
{
        var as = document.getElementsByTagName('a');
        for( var i=0; i&lt;as.length; i++ )
        {
                as[i].onclick = function()
                {
                        return true;
                }
        }
}
&lt;/script&gt;
&lt;style type="text/css"&gt;

&lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;

        &lt;a href="teste.html"&gt;&lt;img src="http://diogoparker.files.wordpress.com/2008/11/13-daylight_planet_wallpaper_by_janedoe873.jpg" alt="" /&gt;&lt;/a&gt;
        &lt;a href="teste.html"&gt;&lt;img src="http://wallpaperslindos.files.wordpress.com/2008/12/outono_wallpaper_by_black_energy.jpg" alt="" /&gt;&lt;/a&gt;
        &lt;a href="teste.html"&gt;&lt;img src="http://fc05.deviantart.com/fs20/f/2007/270/3/4/Balance_Wallpaper_by_nxxos.jpg" alt="" /&gt;&lt;/a&gt;
        &lt;script type="text/javascript"&gt;
        var as = document.getElementsByTagName('a');
        for( var i=0; i&lt;as.length; i++ )
        {
                as[i].onclick = function()
                {
                        return false;
                }
        }
        &lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>



ou seja, o script antes do fechamento do , após todo o HTML, será executado assim que o navegador terminar de ler todo o conteudo em texto, e o script no , condicionado ao window.onload, só rodará qndo o documento tiver completamente carregado. Testa ai