---
id: 2979
title: 'Instalar WordPress no Cloud Server Pro da Locaweb &#8211; Linux'
date: 2013-05-18T14:57:54+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2979
permalink: /linux/instalar-wordpress-no-cloud-server-pro-da-locaweb-linux/
dsq_thread_id:
  - "2105211951"
categories:
  - Linux
tags:
  - cloud
  - ssh
---
[<img src="/wp-content/uploads/2013/05/wordpress-logo.jpg" alt="wordpress-logo" width="800" height="267" class="aligncenter size-full wp-image-2980" srcset="/wp-content/uploads/2013/05/wordpress-logo.jpg 800w, /wp-content/uploads/2013/05/wordpress-logo-300x100.jpg 300w" sizes="(max-width: 800px) 100vw, 800px" />](/wp-content/uploads/2013/05/wordpress-logo.jpg)

São alguns passos simples, mas como não encontrei nenhum tutorial na internet com todos eles, lá vai.

Logicamente, primeiro de tudo, contrate o <a href="http://www.locaweb.com.br/produtos/cloud-server/planos-pro.html" rel="nofollow">Cloud Server Pro</a> no site da Locaweb. Eu aconselho sempre pegar a menor máquina possível. 512mb de RAM, em alguma distribuição Linux que vc se sinta a vontade de trabalhar.

Aqui estou com um Ubuntu.

<!--more-->

## Acesso ssh

A senha padrão do usuário root ssh do teu servidor é a mesma do painel de controle, que vc configurou para o seu usuário durante a contratação.

Abra o seu terminal e digite:

```$ ssh root@cpro9999.publiccloud.com.br```

Sendo o <var>9999</var>, o número da sua máquina que vc encontra no painel do seu cloud.

Coloque a senha e pronto, vc está logado na máquina.

<div class="tab-left">
  <h3>
    Alias de comando no terminal
  </h3>

  ```vim ~/.bash_profile```

  <p>
    Eu uso sempre:
  </p>

  ```alias la="ls -la"```

  <p>
    depois basta recarregar
  </p>

  ```source ~/.bash_profile ```
</div>

<!-- .tab-left -->

<div class="tab-left">
  <h3>
    Instalando dependências
  </h3>

  <p>
    Essa parte é bem simples.
  </p>

  ```$ apt-get update
$ apt-get dist-upgrade
$ apt-get install apache2 mysql-server mysql-client php5 php5-mysql php5-cli libapache2-mod-php5 vim
```

  <div class="tab-left">
    <h4>
      Ativando o php
    </h4>

    <p>
      Se por algum motivo o php não subir automaticamente após a instalação dos pacotes, entre no apache e ative:
    </p>

    ```$ cd /etc/apache2/mods-enabled
$ a2enmod php5```
  </div>

  <p>
    <!-- .tab-left --></div>

    <p>
      <!-- .tab-left -->
    </p>

    <h2>
      Instalando o WordPress
    </h2>

    <p>
      Quanto mais coisas pudermos fazer direto no cloud melhor, pois a conexão lá é violenta de rápida.<br /> Para baixar o wp direto no servidor, basta fazer um <var>wget</var>
    </p>

    <p>
      Direto na pasta <var>/usr/share</var> faça o download da última versão:
    </p>

    ```$ wget http://wordpress.org/latest.zip```

    <p>
      Se não tiver instalado, instale o <var>unzip</var>
    </p>

    ```$ apt-get install unzip```

    <p>
      E ai abra o zip:
    </p>

    ```$ unzip latest.zip```

    <p>
      Ao extrair, a pasta <var>wordpress/</var> será criada. Agora aponte o root do servidor para ela:
    </p>

    ```$ vim /etc/apache2/sites-available/default```

    <p>
      Edite o DocumentRoot para
    </p>

    ```DocumentRoot /usr/share/wordpress```

    <h3>
      Criando o banco
    </h3>

    <p>
      Crie o banco no terminal:
    </p>

    ```$ mysql -u root -pSENHAROOT
mysql> create database wordpress;
```

    <p>
      Acesse no seu browser o IP do seu servidor(vc encontra ele pelo painel do cloud).<br /> Basta rodar normalmente a instalação do wp. Caso o instalador automático não consiga criar o arquivo wp-config.php, volte lá via terminal e crie, dentro de <var>usr/share/wordpress</var>
    </p>

    ```$ vim wp-config.php```

    <p>
      Pronto, tudo instalado e rodando. Falta apenas fazer upload do seu tema.
    </p>

    <div class="tab-left">
      <h3>
        Instalando um servidor ftp
      </h3>

      <p>
        Este artigo é bastante bom:<br /> <a href="http://www.vivaolinux.com.br/artigo/Instalando-e-configurando-um-servidor-FTP/" rel="nofollow">http://www.vivaolinux.com.br/artigo/Instalando-e-configurando-um-servidor-FTP/</a>
      </p>

      ```$ apt-get install proftpd```

      <p>
        Eu confirei o name server do ftp como o endereço do cloud: <var>cpro9999.publiccloud.com.br</var>
      </p>

      <p>
        Assim que terminar de instalar, crie um usuário
      </p>

      ```$ adduser wp```

      <p>
        Basta seguir as instruções.
      </p>

      <p>
        Altere o usuário da pasta themes, que fica dentro de wp-content/
      </p>

      ```chown wp:wp themes```
    </div>

    <p>
      <!-- .tab-left -->
    </p>

    <h4>
      Enviando o tema via ftp
    </h4>

    <p>
      Terminado isso, abra outra aba do seu terminal e permaneça local na sua máquina.<br /> Navegue até encontrar a pasta em que está o seu tema <strong>zipado</strong>, pois ficará mais simples enviar tudo em um só comando.
    </p>

    <p>
      Localmente digite:
    </p>

    ```$ ftp wp@cpro9999.publiccloud.com.br
ftp> ls
ftp> cd /usr/share/wordpress/wp-content/themes```

    <p>
      Assim que eu conecto em algum ftp via terminal, eu sempre mando um <var>ls</var>, apenas para o servidor aceitar minha conexão e ficar rápido.
    </p>

    <p>
      Para verificar em qual diretório vc está local, basta usar <var>lcd</var>, com 2 tabs, será listado o diretório atual local em que vc está.
    </p>

    <p>
      Envie o tema:
    </p>

    ```ftp> put seu_tema.zip seu_tema.zip```

    <p>
      Volte para a aba ssh, extraia o tema do zip e apague o zip
    </p>

    ```$ unzip seu_tema.zip
$ rm seu_tema.zip```

    <p>
      Ative seu tema no painel do WordPress, e parabéns!! está no ar.
    </p>
