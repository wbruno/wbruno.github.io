---
id: 3110
title: 'Efeito mostrar - Botão show/hide área spoiler'
date: 2013-10-16T09:33:35+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3110
permalink: /javascript-puro/efeito-mostrar-botao-showhide-area-spoiler/
dsq_thread_id:
  - "2102923887"
categories:
  - Javascript
---
Poste rápido. Apenas o código mesmo.

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>

<style>
p { margin: 0; }
.spoiler-area {
    border: 1px solid #000;
    padding: 10px;
    height: auto;
}
.spoiler-area.is-closed { height: 0; overflow: hidden; padding: 10px 0 0; }
</style>
</head>
<body>

<strong>Spoiler</strong> <button data-target="spoiler1" class="btn-spoiler">Show</button>
<div id="spoiler1" class="spoiler-area is-closed">
    <p>Mensagem aqui</p>
</div><!-- .spoiler-area -->

<script>
(function(){
    "use strict";
    var $btns = document.querySelectorAll('.btn-spoiler');
    function loop($els, cb) {
        var i = $els.length;
        while(i--) {
            cb($els[i]);
        }
    }
    loop($btns, function($btn){
        $btn.addEventListener("click", function(){
            var $spoiler = document.getElementById(this.getAttribute("data-target"));
            if( this.innerHTML === "Show" ){
                this.innerHTML = "Hide";
                $spoiler.classList.remove("is-closed");
            } else {
                this.innerHTML = "Show";
                $spoiler.classList.add("is-closed");
            }
        });

    });

}());
</script>
</body>
</html>
```
