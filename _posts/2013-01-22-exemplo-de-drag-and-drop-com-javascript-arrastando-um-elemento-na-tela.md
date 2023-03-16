---
id: 2895
title: 'Exemplo de Drag and Drop com javascript &#8211; Arrastando um elemento na tela'
date: 2013-01-22T16:17:11+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2895
permalink: /javascript-puro/exemplo-de-drag-and-drop-com-javascript-arrastando-um-elemento-na-tela/
dsq_thread_id:
  - "2102798563"
categories:
  - Javascript
---
Exemplo rápido com js puro.

Arrastando um elemento atraves de um palco, no eixo x

``` html
/**
  http://www.webreference.com/programming/javascript/mk/column2/index.html
  http://www.youngpup.net/projects/dom-drag/demo.html
 */

<div id="stage">
  <div id="obj" class="fright">
    
  </div><!-- #obj -->
</div><!-- #stage -->
<style type="text/css">
#stage {
  position: relative;
  height: 50px;
  width: 900px;
  margin: 200px auto;
  background: #ff0;
}
#obj {
  background: #f00;
  height: 100px;
  width: 100px;
  position: absolute;
  top: -25px;
  left: 0;
}
.fright { float: right; }
</style>
<script>
var dragObj = null,
i = 0,
stage = document.getElementById('stage'),
obj = document.getElementById('obj');

document.onmousemove = function(e){
  if( dragObj ) {

    if( e.clientX>stage.offsetLeft && e.clientX<(stage.offsetWidth+stage.offsetLeft-obj.offsetWidth) ){
      dragObj.style.left = e.clientX - stage.offsetLeft;
    }
  }
};
document.onmouseup = function(){
  dragObj = null;
};
obj.onmousedown = function(e){
  dragObj = this;
  console.log('down', e);
};

</script>

```

## [Demonstração](http://wbruno.com.br/scripts/slide-draganddrop.html)