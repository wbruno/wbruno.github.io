---
id: 620
title: Resgatar conteúdo de editor rico TinyMCE
date: 2011-04-05T17:18:58+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=620
permalink: /javascript-puro/resgatar-conteudo-de-editor-rico-tinymce/
dsq_thread_id:
  - "2102629704"
categories:
  - Javascript
---
Boas galera!

Passando para deixar uma forma prática e resumida de como fazer isso.

Nem é complicado, ou difícil.. porém já vi vários usuários no fórum precisando.

<!--more-->

``` html
<html>
<head>
<script type="text/javascript" src="tiny_mce/tiny_mce.js"></script>
<script type="text/javascript">
tinyMCE.init({
        theme : "advanced",
        mode : "textareas"
});
window.onload = function(){
        document.getElementById('ok').onclick = function(){
                alert( tinyMCE.get('teste').getContent() );
        }
}
</script>
</head>
<body>
        <textarea name="teste" id="teste">Teste de Texto</textarea>

        <input type="button" name="ok" id="ok" value="ok" />
</body>
</html>
```

a saída vai ser:

``` html
<p>Teste de Texto</p>
```

Única coisa que eu fiz, foi ir na documentação, ler e aplicar

<a href="http://tinymce.moxiecode.com/wiki.php/API3:method.tinymce.Editor.getContent" target="_blank">http://tinymce.moxiecode.com/wiki.php/API3:method.tinymce.Editor.getContent</a>

Porém nem sempre fazer isso ocorre a mente dos nossos colegas de profissão, então fica aqui a dica.

E até se eu precisar responder mais alguém, já tenho o código a mãos.
