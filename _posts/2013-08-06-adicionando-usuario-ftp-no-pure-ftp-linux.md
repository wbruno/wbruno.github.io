---
id: 3057
title: Adicionando usuário ftp no pure-ftp Linux
date: 2013-08-06T07:00:03+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3057
permalink: /wordpress/adicionando-usuario-ftp-no-pure-ftp-linux/
dsq_thread_id:
  - "2102996482"
categories:
  - WordPress
tags:
  - cloud
---
E se você tem acesso SSH ao seu cloud, e precisa adicionar um novo usuário ftp ?

E ai ? **#comofas?**

[<img src="/wp-content/uploads/2013/08/a.png" alt="a" width="444" height="138" class="aligncenter size-full wp-image-3059" srcset="/wp-content/uploads/2013/08/a.png 444w, /wp-content/uploads/2013/08/a-300x93.png 300w" sizes="(max-width: 444px) 100vw, 444px" />](/wp-content/uploads/2013/08/a.png)

<!--more-->

Basta alguns passos simples, mas demorei um pouco para juntar todos eles e fazer tudo funcionar.

Então, vou deixar aqui como fiz:

## Primeiro: adicione um usuário no linux

``` bash
# adduser wp --home /usr/share/wordpress/
```

A sintaxe desse comando é **adduser** <seu_usuario> **-home** <path\_desse\_usuario>

### Depois: Recupere o uid e gid desse usuário

``` bash
# id wp
uid=1000(wp) gid=1000(wp) groups=1000(wp)
```

A sintaxe é bem simples: **id** <seu_usuario>

## E ai: adicione o seu usuário no pure-ftpd

``` bash
# pure-pw useradd wp -u 1000 -g 1000 -d /usr/share/wordpress/
```

E a sintaxe desse aqui é:

``` bash
**pure-pw useradd** <seu_usuario> **-u**<uid\_do\_usuario> **-g**<gid\_do\_usuario> **-d** <path\_raiz\_que\_o\_usuario\_tera\_acesso>
```

Simples assim. Vendo essas 3 linhas de comando super simples, fica tudo muito fácil.

Aproveite, mas comente aqui caso use. =)
