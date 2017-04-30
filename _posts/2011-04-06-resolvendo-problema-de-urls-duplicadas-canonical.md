---
id: 623
title: 'Resolvendo problema de URLs duplicadas &#8211; canonical'
date: 2011-04-06T06:00:15+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=623
permalink: /seo/resolvendo-problema-de-urls-duplicadas-canonical/
categories:
  - SEO
tags:
  - apache
  - htaccess
---
[<img src="http://wbruno.com.br/wp-content/uploads/2011/04/seo-279x300.jpg" alt="" title="seo" width="279" height="300" class="alignright size-medium wp-image-629" srcset="http://wbruno.com.br/wp-content/uploads/2011/04/seo-279x300.jpg 279w, http://wbruno.com.br/wp-content/uploads/2011/04/seo.jpg 300w" sizes="(max-width: 279px) 100vw, 279px" />](http://wbruno.com.br/wp-content/uploads/2011/04/seo.jpg)
  
**SEO** é sempre um assunto que atrai muitos comentários, e atenção.

Dentre as diretivas do google, consta &#8220;<a href="http://www.google.com/support/webmasters/bin/answer.py?hl=pt-BR&#038;answer=66359" target="_blank">Conteudo Duplicado</a>&#8220;.

Existem várias formas de &#8216;cometer&#8217; esse erro, porém uma um pouco complicada de resolver, é não deixar os robôs, acharem que:
  
<u>http://dominio.com.br</u> é diferente de:
  
<u>http://www.dominio.com.br</u>

Com e sem o **www.**, o teu site exibe o mesmo conteúdo.
  
E ainda, que:
  
<u>http://dominio.com.br/index.php</u> é diferente de:
  
<u>http://www.dominio.com.br/</u>

<!--more-->


  
Uma forma bonita de resolver, é usando **redirecionamento 301 com .htaccess**. Dessa forma, informamos para o cliente que estiver solicitando algo ao nosso domínio que: &#8216;o conteúdo que ali estava, foi permanentemente redirecionado&#8217;.

Assim, para os robôs (google, yahoo, bing..) não teremos mais &#8216;conteúdo&#8217; duplicado, mas sim, um que &#8216;era acessado de tal forma&#8217;, e &#8216;foi movido&#8217;. Não ferimos as diretrizes, e garantimos uma melhor consistência na entrega do conteúdo.

No arquivo **.htaccess**(só extensão, sem &#8216;nome&#8217; mesmo), adicione o seguinte conteúdo:

<pre name="code" class="html">RewriteEngine On

RewriteCond %{HTTP_HOST} !^dominio\.com\.br\/index.php$
RewriteRule index.php(.*) http://www.dominio.com.br/$1 [R=301,L]

RewriteRule index.php(.*) http://www.dominio.com.br/$1 [R=301]

RewriteCond %{HTTP_HOST} !^www\.dominio\.com\.br$
RewriteRule (.*) http://www.dominio.com.br/$1 [R=301,L]
</pre>

Substitua **dominio** pelo teu site em questão, atentando para a extensão .COM, .COM.BR.. ou outra do teu domínio.