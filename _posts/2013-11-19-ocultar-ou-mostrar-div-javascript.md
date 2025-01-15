---
id: 3141
title: 'Ocultar ou Mostrar DIV - JavaScript'
date: 2013-11-19T08:00:37+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3141
permalink: /javascript-puro/ocultar-ou-mostrar-div-javascript/
dsq_thread_id:
  - "2102975623"
categories:
  - Javascript
---
``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
<style>
.box {
    width: 200px;
    height: 200px;
    margin-right: 20px;
    background: #000;
    color: #fff;
    font-size: 50px;
    text-align: center;
    line-height: 200px;
}
.fleft { float: left; }
.is-hidden { display: none; }
</style>
</head>
<body>
    <a href="#" class="lnk-show" data-div="1">mostrar</a>
    <a href="#" class="lnk-hide" data-div="1">esconder</a>
    <br />

    <a href="#" class="lnk-show" data-div="2">mostrar</a>
    <a href="#" class="lnk-hide" data-div="2">esconder</a>
    <br />

    <a href="#" class="lnk-show" data-div="3">mostrar</a>
    <a href="#" class="lnk-hide" data-div="3">esconder</a>
    <br />

    <a href="#" class="lnk-show" data-div="4">mostrar</a>
    <a href="#" class="lnk-hide" data-div="4">esconder</a>
    <br />

    <a href="#" class="lnk-show" data-div="5">mostrar</a>
    <a href="#" class="lnk-hide" data-div="5">esconder</a>
    <br />


    <br />

    <div class="box fleft" data-me="1">1</div>
    <div class="box fleft" data-me="2">2</div>
    <div class="box fleft" data-me="3">3</div>
    <div class="box fleft" data-me="4">4</div>
    <div class="box fleft" data-me="5">5</div>

<script>
(function() {
    "use strict";
    /*jslint browser:true*/

    var $boxes = document.getElementsByClassName("box"),
        $lnksShow = document.getElementsByClassName("lnk-show"),
        $lnksHide = document.getElementsByClassName("lnk-hide");


    function loop($els, cb) {
        var i = $els.length;

        while (i > 0) {
            i--;
            cb($els[i]);
        }
    }
    function hideAll($els) {
        loop($els, function($el) {
            $el.classList.add("is-hidden");
        });
    }
    function getDiv(n) {
        return document.querySelector("[data-me='" + n + "']");
    }

    loop($lnksShow, function($lnk) {
        $lnk.addEventListener("click", function(e) {
            e.preventDefault();
            var div = getDiv(this.getAttribute("data-div"));

            hideAll($boxes);

            div.classList.remove("is-hidden");
        });
    });
    loop($lnksHide, function($lnk) {
        $lnk.addEventListener("click", function(e) {
            e.preventDefault();
            var div = getDiv(this.getAttribute("data-div"));

            div.classList.add("is-hidden");
        });
    });


}());
</script>
</body>
</html>
```
