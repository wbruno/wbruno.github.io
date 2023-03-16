---
id: 2071
title: Detectando browser mobile com javascript
date: 2012-06-28T15:04:12+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2071
permalink: /expressao-regular/detectando-browser-mobile-javascript/
dsq_thread_id:
  - "2102060645"
categories:
  - Expressão Regular
---
Boas!!

Eu previsava de uma função que detectasse se o visitante estava utilizando um browser mobile, <a href="http://www.justindocanto.com/scripts/detect-a-user-on-a-mobile-browser-or-device" rel="external nofollow">achei esta aqui na internet</a>:

``` php
function isMobile() {
    return preg_match("/(android|avantgo|blackberry|bolt|boost|cricket|docomo|fone|hiptop|mini|mobi|palm|phone|pie|tablet|up\.browser|up\.link|webos|wos)/i", $_SERVER['HTTP_USER_AGENT']);
}
```

funciona bem, está tecnicamente bem escrita, e resolvia a questão.

Fiz uma versão em javascript, ficou assim:

``` js
/**
 * @function isMobile
 * detecta se o useragent e um dispositivo mobile
 */
function isMobile()
{
  var userAgent = navigator.userAgent.toLowerCase();
  if( userAgent.search(/(android|avantgo|blackberry|bolt|boost|cricket|docomo|fone|hiptop|mini|mobi|palm|phone|pie|tablet|up\.browser|up\.link|webos|wos)/i)!= -1 )
    return true;
}
```

Ambas se baseiam no cabeçalho **user agent** que cada browser envia junto com a requisição http.

O funcionamento é o mesmo nas duas, logicamente não tenho todos esses aparelhos, consegui testar num tablet samsung, no iphone, e em outros 2 androids.

É isso, conseguiu testar com mais algum dispositivo ?

Caso não tenha &#8220;funcionado&#8221;, me envie o user agent dele, para que eu inclua na expressão regular.
