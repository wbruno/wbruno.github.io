---
id: 59
title: onkeyup com delay..
date: 2010-07-14T12:00:04+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=59
permalink: /jquery/onkeyup-com-delay/
categories:
  - jQuery
---
``` html
<html>
<head>
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js"></script>
<script type="text/javascript">
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
</script>
</head>
<body>
        <form action="" method="post">
                <fieldset>
                        <label><input type="text" name="search" /></label>
                </fieldset>
        </form>
</body>
</html>
```
