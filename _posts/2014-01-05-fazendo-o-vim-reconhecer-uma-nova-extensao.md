---
id: 3152
title: Fazendo o vim reconhecer uma nova extensão
date: 2014-01-05T22:26:46+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3152
permalink: /html/fazendo-o-vim-reconhecer-uma-nova-extensao/
dsq_thread_id:
  - "2101919446"
categories:
  - HTML
tags:
  - terminal
  - vim
---
Boas!

Estou fazendo um projetinho de um site estático em NodeJS com handlebars.

Mas os arquivos partials com extensão **.hbs** não foram reconhecidos pelo vim como arquivos html. Então, para o highlight funcionar, tive que adicionar o hbs como um html.

Encontrei a resposta nesse link:

<a href="http://vim-anotacoes.blogspot.com.br/2009/04/adicionando-um-novo-tipo-de-arquivo.html" rel="nofollow">Fazendo o vim reconhecer um novo tipo de arquivo pela extensão</a>

`vim ~/.vim/filetype.vim `

``` bash
augroup filetypedetect
au BufNewFile,BufRead *.hbs setf html
augroup END
```

É isso! =)

Vim FTW!
