---
id: 2175
title: 'Usando apt-get instal - remove no MAC OSx Mountain Lion'
date: 2012-07-29T03:25:23+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2175
permalink: /mac/usando-apt-get-instal-remove-no-mac-osx-mountain-lion/
dsq_thread_id:
  - "2101157902"
categories:
  - MAC
---
Opa!

Acabei agorinha de instalar no meu mac o gerenciador de pacotes **fink**.

Este link aqui, explica bem os passos:

<a href="http://www.finkproject.org/download/srcdist.php" rel="external nofollow">http://www.finkproject.org/download/srcdist.php</a>

Mas como tenho memória curta, vou deixar escrito aqui, os outros passos que tive que fazer.

Primeiro de tudo, tive que instalar um compilador da Linguagem C, pois ele veio desligado no xCode.

E isto eu consegui com ajuda deste outro link:

<a href="http://www.macobserver.com/tmo/article/install_the_command_line_c_compilers_in_os_x_lion/" rel="external nofollow">http://www.macobserver.com/tmo/article/install_the_command_line_c_compilers_in_os_x_lion/</a>

Agora sim, rodando o instalador depois de ter compilado o fink, teremos que instalar o **x11**.

E ele se encontra neste link:

<a href="http://xquartz.macosforge.org/landing/" rel="external nofollow">http://xquartz.macosforge.org/landing/</a>

é isso. Os passos intermediários estão nestes links. Pode deixar a configuração padrão do fink.

Feito isso, vc já poderá fazer

apt-get update, apt-get install, dpkg -list&#8230; e outras coisas direto no terminal do teu mac.
