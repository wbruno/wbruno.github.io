---
id: 2932
title: 'Plugin jQuery.maskx - Mascara javascript de campos com expressão regular - regex'
date: 2013-03-26T08:00:06+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=2932
permalink: /jquery/plugin-jquery-mask-mascara-javascript-de-campos-com-expressao-regular-regex/
dsq_thread_id:
  - "2104711969"
categories:
  - jQuery
tags:
  - máscara
---
Opa,

Esse post é para divulgar um novo repositório que criei no github.

[<img src="/wp-content/uploads/2013/03/url.png" alt="url" width="580" height="230" class="aligncenter size-full wp-image-2933" srcset="/wp-content/uploads/2013/03/url.png 580w, /wp-content/uploads/2013/03/url-300x118.png 300w" sizes="(max-width: 580px) 100vw, 580px" />](/wp-content/uploads/2013/03/url.png)

<a href="https://github.com/wbruno/jquery.mask" rel="external nofollow" target="_blank">https://github.com/wbruno/jquery.mask</a>.

É um plugin jQuery que escrevi com base nestas [máscaras com expressão regular](https://wbruno.com.br/expressao-regular/diversas-mascaras-com-er/), e esse plugin já inclui a função de [máscara javascript de cartões de crédito](https://wbruno.com.br/expressao-regular/mascara-cartao-de-credito-com-javascript-e-expressao-regular-regex/).

## Exemplo de uso

``` js
jQuery.fn.maskx.user_defined = function(v){
  v = v.replace(/\D/g, "");
  v = v.replace(/(\d{3})(\d)/, "$1/$2");
  v = v.replace(/(\d+)(\d{2})$/, "$1-$2");
  return v;
};
jQuery(document).ready(function(){
    jQuery('input[name^="NumeroCC"]').maskx({maskx: 'cc'});
    jQuery('input[name="cep"]').maskx({maskx: 'cep'});

    jQuery('input[name="dinheiro"]').maskx({maskx: 'money'});


    jQuery('input[name="other"]').maskx({maskx: 'user_defined'});
});
```

É isso galera, usem lá. E me digam o que acharam. Além de abrirem suas issues e pull requests.
