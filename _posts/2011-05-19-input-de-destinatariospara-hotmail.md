---
id: 968
title: 'Input de destinatários[para] do hotmail'
date: 2011-05-19T07:00:10+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=968
permalink: /css/input-de-destinatariospara-hotmail/
categories:
  - CSS
---
Sempre achei &#8216;bonito&#8217;, o input onde adicionamos os destinatários no hotmail.

Um dia, estava &#8216;sem fazer muita coisa&#8217;, e resolvi reproduzir o efeito daquele input.

[<img src="/wp-content/uploads/2011/05/input.jpg" alt="" title="input" width="767" height="135" class="aligncenter size-full wp-image-969" srcset="/wp-content/uploads/2011/05/input.jpg 767w, /wp-content/uploads/2011/05/input-300x52.jpg 300w" sizes="(max-width: 767px) 100vw, 767px" />](/wp-content/uploads/2011/05/input.jpg)

<!--more-->

**index.html**

``` html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <title>Input Hotmail</title>
  <link type="text/css" href="main.css" rel="stylesheet" />
  <!--[if IE 6]>
  <style type="text/css">
  #emails #cntmail { top: 3px; left: 74px; }
  </style>
  <![endif]-->
</head>
<body>
  <form action="" method="post">
    <fieldset>
      <label id="meu">meu_email@hotmail.com <img src="seta.gif" alt="" /></label>
      <label id="emails"><span>Para: </span>
        <input type="text" name="email" />
          <span id="cntmail">
            <span>email@provedor.com
              <img src="edit.gif" alt="" class="edit" />
              <img src="del.gif" alt="" class="del" />
            </span>
          </span>
      </label><!-- /emails -->
      <label><span>Assunto: </span>
        <input type="text" name="assunto" /></label>
    </fieldset>
  </form>


</body>
</html>
```

**main.css**

``` css
* {
  margin: 0;
  padding: 0;
  list-style: none;
  border: none;
}
body {
  font: 13px Tahoma, Arial, sans-serif;
  margin: 50px;
}
fieldset {
  border: 1px solid #cbcbcb;
  padding: 10px 15px;
}
label {
  display: block;
  padding-left: 20px;
  margin: 1px;
}
label span {
  width: 50px;
  display: inline-block;
  text-align: right;
}
input {
  background: #fff;
  font: 13px Tahoma, Arial, sans-serif;
  border: 1px solid #cbcbcb;
  width: 600px;
  padding: 2px 5px;
  color: #2a2a2a;
  height: 20px;
  margin-left: 2px;
}
#meu {
  color: #2a2a2a;
  font-size: 19px;
  padding: 0 0 5px 0;
}
#emails {
  position: relative;
  height: 30px;
}
#emails input {
  padding-left: 165px;
  width: 440px;
}
#emails #cntmail {
  position: absolute;
  top: 2px;
  left: 78px;
  width: auto;
}
#cntmail span {
  border: 1px solid #bbd8fb;
  background: #f3f7fd;
  color: #2a2a2a;
  padding: 2px 5px;
  width: auto;
}
#cntmail img {
  cursor: pointer;
}
```

Cada destinatário, é um <span> dentro do **span#cntmail**. Cada vez que adicionarmos um email &#8216;no input&#8217;, precisamos aumentar o padding-left dele, para que a digitação do próximo email comece após os emails já adicionados.

## <a href="http://www.wbruno.com.br/scripts/msn/" target="_blank">Demonstração Online</a>
