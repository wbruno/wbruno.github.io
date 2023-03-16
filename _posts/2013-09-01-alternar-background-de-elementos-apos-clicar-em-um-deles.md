---
id: 3072
title: Alternar background de elementos após clicar em um deles
date: 2013-09-01T11:41:27+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3072
permalink: /javascript-puro/alternar-background-de-elementos-apos-clicar-em-um-deles/
dsq_thread_id:
  - "2104079953"
categories:
  - Javascript
---
**Situação:** dado um certo número de elementos, ao clicar em algum deles, este deve ganhar um background color, porém os demais elementos irmãos dessse, devem &#8220;perder&#8221;, e voltar para o estado original.

**Algoritmo:** remover o estado _de todos_ os elementos antes de adicionar naquele que vc clicou.

**Código:** criei uma função loop(), apenas para iterar sobre os elementos. O restante é bem básico. Uma variável para cachear todos os elementos com a class .box, e um addEventListener para colocar a função no onclick deles.

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>

    <script src="//polyfill.io/"></script>
<style>
.is-active { background: #f00; }
</style>
</head>
<body>

    <div id="box1" class="box">Clique aqui</div>
    <div id="box2" class="box">Clique aqui</div>
    <div id="box3" class="box">Clique aqui</div>
    <div id="box4" class="box">Clique aqui</div>


<script>
(function () {
    "use strict";
    /*jslint browser: true */

    var $boxes = document.querySelectorAll('.box'),
        loop = function ($els, cb) {
            var i = $els.length;

            while (i > 0) {
                i -= 1;
                cb($els[i]);
            }
        },
        resetBg = function ($els) {
            loop($els, function ($el) {
                $el.classList.remove('is-active');
            });
        };

    loop($boxes, function ($box) {
        $box.addEventListener('click', function () {

            resetBg($boxes);

            this.classList.add('is-active');
        }, false);
    });

}());
</script>
</body>
</html>
```