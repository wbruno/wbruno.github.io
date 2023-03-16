---
id: 3156
title: 'Enviando arquivos via rsync &#8211; MAC'
date: 2014-01-17T16:08:00+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3156
permalink: /mac/enviando-arquivos-via-rsync-mac/
categories:
  - MAC
tags:
  - terminal
---
Se &#8220;não podemos&#8221; usar ftp, então podemos usar o quê ?

Rimou ne?! =)

Tirando as piadas de graça de lado, uma ótima alternativa é usar **rsync**.

``` bash
rsync -Cravzp images/ user@server.com.br:/var/www/site/public/images/
```

Eu usei a linha acima para syncronizar uma pasta local com outra no servidor ssh. Levou 1 segundo para enviar 1 mega de imagens.

``` bash
building file list ... done
./
selo-valor-strudel-115.png
selo-valor-strudel-50.png
selo-valor-strudel-55.png
selo-valor-strudel-60.png
selo-valor-strudel-75.png
selo-valor-strudel-80.png

sent 86441 bytes  received 158 bytes  173198.00 bytes/sec
total size is 87483  speedup is 1.01
```

E o legal, é que se as imagens não tiverem modificações:

``` bash
building file list ... done
./
.DS_Store

sent 584 bytes  received 48 bytes  1264.00 bytes/sec
total size is 93631  speedup is 148.15
```

Ele não envia nada. E ai ? qual a sua desculpa para continuar usando ftp ? e pior, em um programa visual ?

Terminal com rsync!!
