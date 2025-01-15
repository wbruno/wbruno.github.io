---
id: 3457
title: 'Como viver com pouco HD - Macbook 128GB SSD'
date: 2015-10-10T00:31:09+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=3457
permalink: /mac/como-viver-com-pouco-hd-macbook-128gb-ssd/
categories:
  - MAC
---
Eu tenho um Macbook Pro retina, com hd 128GB SSD. Pouco HD. Mas nem por isso, não quer dizer que não seja possível fazer um bom uso, otimizando ao máximo o que pudermos.

Nesse post vou listar algumas maneiras de limpar o teu HD, para sobrar mais espaço no disco de boot, assim não prejudicando a performance da máquina.

<img src="/wp-content/uploads/2015/10/startup-disk-full-free-space.jpg" alt="startup-disk-full-free-space" width="443" height="198" class="aligncenter size-full wp-image-3470" srcset="/wp-content/uploads/2015/10/startup-disk-full-free-space.jpg 443w, /wp-content/uploads/2015/10/startup-disk-full-free-space-300x134.jpg 300w" sizes="(max-width: 443px) 100vw, 443px" />

**Apesar da maioria das dicas que vou dar serem seguras, e eu mesmo ter feito na minha máquina, NÃO ME RESPONSABILIZO por eventuais danos.** Seja cuidadoso e entenda o que está fazendo. Se tiver dúvidas, não prossiga!!

<!--more-->

Lembre-se **sempre** de versionar os teus projetos no GIT.

## Identifique

Uma forma bem simples e eficaz de encontrar onde estão os teus maiores diretórios, é através do Time Machine. Dê um <var>Command + Space</var> -> Time Machine, e depois <var>Command + ,</var>.

Assim que eu descobri que tenho agora 16GB no Applications e 10GB na Music.

O comando **du** (disk usage), também é bem útil para encontrar grandes diretórios.

```
$ sudo du -ah ~ | sort -rn | head -20
```

```
$ find / -size +100M -ls
```

## Remova programas não utilizados

Como o **Postgres, Vagrant** por exemplo.. remove aqueles softwares que você nunca mais usou.. (básico).

Aqui ainda vale a dica de remover o iMove, o GarageBand, etc. (aqueles apps que vem instalados e ninguém usa..)

## Instale o CleanMyMac 2/3

Já uso esse programa a alguns anos, ele é muito bom. Deixe ele fazer o trabalho dele, além de remover **LeftLovers** (arquivos esquecidos de programas removidos), otimizar álbuns de fotos, etc.

## Apague a pasta ~/Downloads e os *.dmg

Uma vez baixado e instalado, você não precisa mais do dmg ou de algo que fique na Downloads. Costumo manter a minha Lixeira e a Downloads vazias.

```
$ sudo find / -name "*.dmg" > log
cat log
```

## Apague os backups do iPhone

Se você tem costume de conectar teu iPhone no Mac, pode ser que esteja gerando gigas e gigas de backups na tua máquina. Dentro do iTunes, aperte <var>Command + ,</var>. Vá em **Devices**, e apague os backups.

É muito melhor deixar eles no **iCloud** do que no disco local. Outra vantagem de deixar no iCloud é que o backup na nuvem é compatível com qualquer versão de iOS que você instalar. Então, não terá dores de cabeça para testar Betas, GMs ou Novas versões, e o backup não puder ser restaurado por incompatibilidade.

Deixe os backups na nuvem!!

## Backup da máquina em HD externo

O ponto acima me lembra de dizer: faça backup da tua máquina em um HD externo! Nem preciso explicar muito isso ne?! configure o Time Machine para apontar para um HD externo.

Feito isso, é interessante que caso queira baixar algum torrent, ele também vá direto para o HD, não tem porque passar pela tua máquina&#8230;

## Apague /~Library/MobileDevice/Software\ Images/

Facilmente terá alguns arquivos de alguns gigas nessa pasta. Delete.

```
rm ~/Library/MobileDevice/Software\ Images/iPhone5,1_7.0_11A4372q_Restore.ipsw
rm -r ~/Library/Developer/Xcode/Archives/*
rm -r ~/Library/Developer/Xcode/DerivedData/*
```

Veja os caches:

```
$ ls -lh ~/Library/Caches/
```

Podem existir alguns backups *.ipa, também:

```
$ rm -r ~/Music/iTunes/iTunes\ Media/Mobile\ Applications/*
```

## Mail Downloads

Apague o conteúdo da pasta Mail Downloads. Conforme você for lendo emails, recebendo anexos, abrindo, fazendo downloads, essa pasta vai guardando um &#8220;cache&#8221; deles. Pode limpar tranquilamente.

```
$ ll ~/Library/Containers/com.apple.mail/Data/Library/Mail\ Downloads/
```

## Archive do iChat/iMessage

Esse eu nem sabia que existia.. por ser apenas texto é relativamente leve, apenas alguns MegaBytes.

```
$ rm -r /Users/wbruno/Library/Containers/com.apple.iChat/Data/Library/Messages/Archive/*
```

## Remova versões antigas de linguagens

Seja do Ruby, NodeJS, Java.. você pode acabar com várias versões antigas que nem quer utilizar mais instaladas na tua máquina. Remove as versões antigas.

NodeJS

```
$ sudo n rm io 3.2.0
$ sudo n rm 4.0.0
```

Java

```
ll ~/Library/Application\ Support/Java/
```

Ahh!! e se você está usando algum gerenciador de versões como o N ou o NVM, apague a instalação default do teu NodeJS:

```
$ yes | rm -r /usr/local/include/node/
```

Verifique em /usr/local/n/versions se existem mais instalações:

```
rm -r /usr/local/n/versions/0.10.3*
```

## Use o iMatch

o iMatch é um serviço no Cloud da Apple que mantém as tuas músicas na nuvem. Você pode ouvi-las via streaming ou via arquivos locais. Deixe aquelas músicas que você não ouve sempre, fora da máquina local. Aqui eu consegui reduzir de 20GB para 7GB de Músicas.

Assim como as fotos, também é interessante guardá-las naquele HD externo.

Filmes..

## Apagar bancos de dados antigos do MongoDB

```
$ cd /usr/local/var/mongodb # ou cd /data/db
$ ls -la
```

Veja se há algum &#8220;muito antigo&#8221; ou que não faz mais sentido para você, e apague com <var>rm -r</var>.

## Apagando o OSx anterior

O OSx guarda pedaços do sistema anterior após você atualizar para uma nova versão. Se está tudo ok com o update, e você não sentiu falta de nada, apague esse diretório de alguns GBs:

```
sudo rm -rf /Previous\ System/
```

## Mantenha o brew atualizado

Não é bem uma dica para economizar espaço, mas sempre bom lembrar:

```
$ brew update
$ brew upgrade
```

## Use o Disk Utility

<var>Command + Space</var> -> Disk Utility. Sempre repare as permissões e execute o &#8220;First Aid&#8221;.

## Instale o Disk Discovery X

Uma ótima ferramenta para listar e ver quais as maiores pastas do seu sistema.

No fim das contas, não é nenhum sofrimento tão grande assim.. e 128GB são bem suficientes.. =)

[Conforme eu lembrar de mais alguma coisa, eu volto aqui e adiciono].

<img src="/wp-content/uploads/2015/10/disk-1024x621.png" alt="disk" width="788" height="478" class="aligncenter size-large wp-image-3503" srcset="/wp-content/uploads/2015/10/disk-1024x621.png 1024w, /wp-content/uploads/2015/10/disk-300x182.png 300w, /wp-content/uploads/2015/10/disk-788x478.png 788w, /wp-content/uploads/2015/10/disk.png 1264w" sizes="(max-width: 788px) 100vw, 788px" />


Update:

Atualizei meu macOS para 10.13, e achei um menu que mostra o seguinte:

<img src="/wp-content/uploads/2017/06/storage-mac.png" alt="" class="aligncenter size-large wp-image-3503" />

podendo até deletar alguns arquivos diretamente por aqui.


