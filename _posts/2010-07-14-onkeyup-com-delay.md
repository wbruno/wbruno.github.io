---
id: 59
title: onkeyup com delay..
date: 2010-07-14T12:00:04+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=59
permalink: /jquery/onkeyup-com-delay/
categories:
  - jQuery
---
<pre name="code" class="javascript">&lt;html>
&lt;head>
&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js">&lt;/script>
&lt;script type="text/javascript">
$(document).ready(function(){
        var intervalo = 0;
        $("input[name='search']").keyup(function(){

                clearInterval( intervalo );//ou clearTimeout()
                intervalo = window.setTimeout( ajax, 1500 );
        });
});
function ajax()
{
        alert( 'Agora pode ir executar' );
}
&lt;/script>
&lt;/head>
&lt;body>
        &lt;form action="" method="post">
                &lt;fieldset>
                        &lt;label>&lt;input type="text" name="search" />&lt;/label>
                &lt;/fieldset>
        &lt;/form>
&lt;/body>
&lt;/html>
</pre>