---
id: 3141
title: 'Ocultar ou Mostrar DIV &#8211; JavaScript'
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
<pre>&lt;!doctype html>
&lt;html lang="en">
&lt;head>
    &lt;meta charset="UTF-8">
    &lt;title>Document&lt;/title>
&lt;style>
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
&lt;/style>
&lt;/head>
&lt;body>
    &lt;a href="#" class="lnk-show" data-div="1">mostrar&lt;/a>
    &lt;a href="#" class="lnk-hide" data-div="1">esconder&lt;/a>
    &lt;br />

    &lt;a href="#" class="lnk-show" data-div="2">mostrar&lt;/a>
    &lt;a href="#" class="lnk-hide" data-div="2">esconder&lt;/a>
    &lt;br />

    &lt;a href="#" class="lnk-show" data-div="3">mostrar&lt;/a>
    &lt;a href="#" class="lnk-hide" data-div="3">esconder&lt;/a>
    &lt;br />

    &lt;a href="#" class="lnk-show" data-div="4">mostrar&lt;/a>
    &lt;a href="#" class="lnk-hide" data-div="4">esconder&lt;/a>
    &lt;br />

    &lt;a href="#" class="lnk-show" data-div="5">mostrar&lt;/a>
    &lt;a href="#" class="lnk-hide" data-div="5">esconder&lt;/a>
    &lt;br />


    &lt;br />

    &lt;div class="box fleft" data-me="1">1&lt;/div>
    &lt;div class="box fleft" data-me="2">2&lt;/div>
    &lt;div class="box fleft" data-me="3">3&lt;/div>
    &lt;div class="box fleft" data-me="4">4&lt;/div>
    &lt;div class="box fleft" data-me="5">5&lt;/div>

&lt;script>
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
&lt;/script>
&lt;/body>
&lt;/html>
</pre>