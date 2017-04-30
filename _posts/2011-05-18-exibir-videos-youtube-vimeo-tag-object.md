---
id: 956
title: 'Exibir videos Youtube e Vimeo com a tag &lt;object&gt;'
date: 2011-05-18T07:00:32+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=956
permalink: /html/exibir-videos-youtube-vimeo-tag-object/
dsq_thread_id:
  - "2100808578"
categories:
  - HTML
tags:
  - youtube
---
Se estivermos trabalhando nossos sites com DTD xHTML, não podemos usar a tag <iframe>, então a saída, é embedar com a tag <object>, que funciona muito bem, e valida no w3c.

Apesar do Youtube hoje em dia, só fornecer o embed com iframe, antigamente o código que ele disponibilizava, era baseado nas tags <object>, e <embed>. Acredito que por questões de compatibilidade, ainda hoje conseguimos servir videos do Youtube nos nossos sites, usando a tag object apenas.

<!--more-->

<pre name="code" class="html">&lt;object height="196" width="305" data="http://www.youtube.com/v/HiaOFOMPOBc" type="application/x-shockwave-flash">
                &lt;param name="wmode" value="transparent" />
                &lt;param name="quality" value="hight" />
                &lt;param name="src" value="http://www.youtube.com/v/HiaOFOMPOBc" />
        &lt;/object>
</pre>

No embed do YT, convém notar o formato com que o atributo **data**, e o **value** do param src, devem ser passados.
  
O link no youtube para o vídeo é do tipo: <u>http://www.youtube.com/watch?v=</u>**HiaOFOMPOBc**
  
Sendo o valor que destaque ali em negrito o ID dele.

Para fazer o embed corretamente, vc deve extrair esse ID, e jogar no novo formato da URL: <u>http://www.youtube.com/v/</u>ID\_DO\_VIDEO_AQUI

Já para o vimeo, o buraco é um pouco mais embaixo

<pre name="code" class="html">&lt;object height="196" width="305" type="application/x-shockwave-flash" class="" data="http://a.vimeocdn.com/p/flash/moogaloop/5.1.14/moogaloop.swf?v=1.0.0" style="visibility: visible;">

        &lt;param name="allowscriptaccess" value="always">
        &lt;param name="allowfullscreen" value="true">
        &lt;param name="scalemode" value="noscale">
        &lt;param name="quality" value="high">
        &lt;param name="wmode" value="opaque">
        &lt;param name="bgcolor" value="#000000">
        &lt;param name="flashvars" value="server=vimeo.com&player_server=player.vimeo.com&cdn_server=a.vimeocdn.com&embed_location=&force_embed=0&force_info=1&moogaloop_type=moogaloop_local&js_api=1&js_getConfig=player23465729_920282954.getConfig&js_setConfig=player23465729_920282954.setConfig&clip_id=23465729&fullscreen=1&js_onLoad=player23465729_920282954.player.moogaloopLoaded&js_onThumbLoaded=player23465729_920282954.player.moogaloopThumbLoaded">

&lt;/object>
</pre>

ali nos **flasvars**, dê uma atenção especial ao parâmetro: **clip_id=17100311**, alterando esse ID, vc consegue alterar o vídeo que será exibido no teu embed.

É isso =)