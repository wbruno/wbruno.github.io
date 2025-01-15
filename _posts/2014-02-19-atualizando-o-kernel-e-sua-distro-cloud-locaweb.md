---
id: 3230
title: 'Atualizando o kernel e sua distro - Cloud Locaweb'
date: 2014-02-19T08:00:11+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=3230
permalink: /linux/atualizando-o-kernel-e-sua-distro-cloud-locaweb/
categories:
  - Linux
tags:
  - ssh
  - terminal
---
<img src="/wp-content/uploads/2014/02/debian-1440x900.jpg" alt="debian-1440x900" width="800" height="300" class="aligncenter size-full wp-image-3240" />

<!--more-->

## Atualizando o kernel

``` bash
# rm -f /boot/grub/device.map
# apt-get install linux-image-3.2.0-0.bpo.4-amd64 --reinstall
```

Pois no meu caso, era a imagem que eu tinha disponível:

``` bash
# dpkg -l | grep linux
```

## Atualizando o debian

Os passos abaixo apenas são necessários se mesmo após a atualização do kernel, a distro ainda não está indo para a 7. Caso seja, vamos forçar informando de onde queremos que o sistema busque os pacotes.

Se vc tiver problemas para rodar o upgrade, leia esse cara:

<a href="http://unkmonik.wordpress.com/2012/10/10/pv1-check-your-device-map/" rel="nofollow">FIxed : grub-probe: error: Couldn’t find PV pv1. Check your device.map.</a>

E ai:

``` bash
# cat /etc/debian_version
6.0.8
```

Estou na última versão do debian squeezze

<http://www.debian.org/releases/squeeze/>

Se eu quiser ir para o wheezy <var>vim /etc/apt/sources.list</var>

[Debian Linux: Upgrade v6.0.x Squeeze to v7.0.0 Wheezy](http://www.cyberciti.biz/faq/howto-debian-linux-upgrade-6-squeeze-to-7-wheezy/)

``` bash
deb http://mirrors.kernel.org/debian/ wheezy main
deb-src http://mirrors.kernel.org/debian/ wheezy main

deb http://security.debian.org/ wheezy/updates main
deb-src http://security.debian.org/ wheezy/updates main

# wheezy-updates, previously known as 'volatile'
deb http://mirrors.kernel.org/debian/ wheezy-updates main
deb-src http://mirrors.kernel.org/debian/ wheezy-updates main
```

E ai rodo a atualização

``` bash
apt-get update
apt-get upgrade
apt-get dist-upgrade
```

E se quiser:

``` bash
apt-get autoremove
```

Uma coisa bacana para usar, caso vc tenha problemas com algum pacote, ou ele não esteja instalando corretamente é:

``` bash
apt-get purge pacote-tal
```
