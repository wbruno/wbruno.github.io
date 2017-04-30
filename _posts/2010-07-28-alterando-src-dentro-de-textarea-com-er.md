---
id: 66
title: Alterando src dentro de textarea com ER
date: 2010-07-28T01:04:34+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=66
permalink: /javascript-puro/alterando-src-dentro-de-textarea-com-er/
categories:
  - Javascript
---
<pre name="code" class="html">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"&gt;
&lt;html xmlns="http://www.w3.org/1999/xhtml" xml:lang="pt-br" lang="pt-br"&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
function id( el ){
        return document.getElementById( el );
}
window.onload = function(){
        var imgs = document.getElementsByTagName('img');
        for( var i=0; i&lt;imgs.length; i++ ){
                imgs[i].onclick = function(){
                        var area = id('area').value;                    
                        id('area').value = area.replace(/src="[-a-zA-Z0-9:_\/.]+"/, 'src="'+this.src+'"' );
                }
        }
}
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
        &lt;form action="" method="post"&gt;
                &lt;fieldset&gt;
                &lt;label&gt;&lt;textarea cols="30" rows="7" id="area"&gt;&lt;a href="http://www.site.com.br/index.php?user=2"&gt;&lt;img src="../imagens/imagem.png" alt="" /&gt;&lt;/a&gt;&lt;/textarea&gt;&lt;/label&gt;
                &lt;/fieldset&gt;
        &lt;/form&gt;
       
        &lt;img src="http://100grana.files.wordpress.com/2008/11/mickey-mouse-c.jpg" alt="" /&gt;
        &lt;img src="http://pcmeira.blog.uol.com.br/images/PatoDonald_pcmeira.jpg" alt="" /&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>