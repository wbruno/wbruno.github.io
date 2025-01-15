---
id: 3509
title: package.json entendendo os scripts
date: 2015-11-16T11:43:51+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=3509
permalink: /nodejs/package-json-entendendo-os-scripts/
categories:
  - NodeJS
---
O arquivo **package.json** é o ponto de partida de qualquer projeto NodeJS. Ele é responsável por descrever o seu projeto, informar as engines (versão do node e do npm), url do repositório, versão do projeto, dependências de produção e de desenvolvimento dentre outras coisas.

Uma seção interessante do **package.json**, é a **scripts**. Que será o foco desse post. Veremos como utilizá-la para criar alias para nossos comandos, assim como também fazer um melhor uso dessa funcionalidade.

<img src="/wp-content/uploads/2015/11/package-json-1024x389.png" alt="package json" width="788" height="299" class="aligncenter size-large wp-image-3518" srcset="/wp-content/uploads/2015/11/package-json-1024x389.png 1024w, /wp-content/uploads/2015/11/package-json-300x114.png 300w, /wp-content/uploads/2015/11/package-json-788x299.png 788w, /wp-content/uploads/2015/11/package-json.png 1500w" sizes="(max-width: 788px) 100vw, 788px" />

<!--more-->

## scripts do package.json

A seção scripts possui algumas tarefas padrões como: **start, test, install..**. ([documentação](https://docs.npmjs.com/misc/scripts)).

Após criar um package.json com ajuda do <var>$ npm init -yes</var>, a forma de uso é a seguinte:

``` shell
$ npm test

> t@1.0.0 test /Users/wbruno/Sites/t
> echo "Error: no test specified" && exit 1

Error: no test specified
npm ERR! Test failed.  See above for more details.
```

e irá executar o que tiver definido no json:

``` json
{
  "name": "t",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "William Bruno <wbrunom @gmail.com> (http://wbruno.com.br)",
  "license": "ISC"
}
```

No nosso caso, por enquanto é apenas um **echo**, e um **exit 1** para indicar um erro de que nenhum teste foi definido ainda.

Mas poderia ser a execução do **mocha**, ficando assim:

``` json
"scripts": {
  "test": "_mocha test/node/*"
},

```

E todo script do package, pode ser antecedido por outro que contenha o prefixo **pre**. Se eu quiser executar o jshint antes de executar o mocha, posso deixar o scripts assim:

``` json
"scripts": {
  "pretest": "jshint *"
  "test": "_mocha test/node/*"
},

```

E executar apenas com <var>$ npm test</var>. Okay ?

Assim como para criar scripts personalizados, basta dar qualquer nome, e executar com

``` shell
$ npm run qqcoisa
```

``` json
"scripts": {
  "qqcoisa": "echo 'Qualquer coisa'"
},

```

E o **pre**qqcoisa continua valendo.

Pense que o scripts pode executar qualquer comando de terminal válido. O que você faria na linha de comando, em shell, ou invocando outro script nodejs, pode ficar simplificado, com um apelido no teu package.

## Complicando o package.json

Se um dia você tiver que trabalhar com o Oracle no seu projeto NodeJS, você vai notar que precisa definir uma série de variáveis de ambiente, para que o módulo npm de conexão com o Oracle, saiba onde o instantclient está instalado na sua máquina.

O que pode levar o teu scripts do package ficar gigantesco:

``` json
"scripts": {
  "start": "export OCI_HOME=/opt/instantclient_11_2/ && export OCI_LIB_DIR=$OCI_HOME && export OCI_INC_DIR=$OCI_HOME/sdk/include && export OCI_VERSION=11 && export NLS_LANG=AMERICAN_AMERICA.UTF8 && export DYLD_LIBRARY_PATH=$OCI_HOME && export LD_LIBRARY_PATH=$OCI_HOME && export DEBUG=musashi:* && export NODE_ENV=development && nodemon bin/www",
  "qa": "export OCI_HOME=/opt/instantclient_11_2/ && export OCI_LIB_DIR=$OCI_HOME && export OCI_INC_DIR=$OCI_HOME/sdk/include && export OCI_VERSION=11 && export NLS_LANG=AMERICAN_AMERICA.UTF8 && export DYLD_LIBRARY_PATH=$OCI_HOME && export LD_LIBRARY_PATH=$OCI_HOME && export DEBUG=musashi:* && export NODE_ENV=qa && nodemon bin/www",
  "stg": "export OCI_HOME=/opt/instantclient_11_2/ && export OCI_LIB_DIR=$OCI_HOME && export OCI_INC_DIR=$OCI_HOME/sdk/include && export OCI_VERSION=11 && export NLS_LANG=AMERICAN_AMERICA.UTF8 && export DYLD_LIBRARY_PATH=$OCI_HOME && export LD_LIBRARY_PATH=$OCI_HOME && export DEBUG=musashi:* && export NODE_ENV=stg && nodemon bin/www",
  ...
 }

```

Note que eu tenho uma repetição de **export**, pois no meu package eu posso escolher subir o projeto como desenvolvimento local (start), apontando para as configurações de QA ou de Stage (ambiente pré produção).

### Criando um start.sh

Por isso, que é uma boa idéia criar um arquivo externo para abstrair esses comandos shell, ficando assim **scripts/start.sh**:

``` shell
#!/bin/bash

case "$(uname -s)" in
  Darwin)
    echo 'Mac OS X'
    export OCI_HOME=/opt/instantclient_11_2/
    export OCI_LIB_DIR=$OCI_HOME
    export OCI_INC_DIR=$OCI_HOME/sdk/include
    export OCI_VERSION=11
    export NLS_LANG=AMERICAN_AMERICA.UTF8
    export DYLD_LIBRARY_PATH=$OCI_HOME
    export LD_LIBRARY_PATH=$OCI_HOME
    export DEBUG=musashi:*
  ;;
  Linux)
    echo 'Linux'
    export OCI_LIB_DIR=/usr/lib/oracle/11.2/client64/lib
    export OCI_INC_DIR=/usr/include/oracle/11.2/client64/
    export OCI_INCLUDE_DIR=/usr/include/oracle/11.2/client64/
    export OCI_VERSION=11
    export NLS_LANG=AMERICAN_AMERICA.UTF8
    export LD_LIBRARY_PATH=/usr/lib/oracle/11.2/client64/lib
  ;;
  *)
    echo 'Unsupported OS'
    exit 1
esac

case "$1" in
  test-api)
    export NODE_ENV=jenkins
    node_modules/istanbul/lib/cli.js cover --dir ./coverage-api --hook-run-in-context node_modules/mocha/bin/_mocha test/api/*
  ;;
  jshint)
    node_modules/jshint/bin/jshint app.js bin/www controllers/* db/* models/* routes/* test/* util/* src/js/* jobs/*
  ;;
  coverage)
    export NODE_ENV=test
    node_modules/istanbul/lib/cli.js cover --hook-run-in-context node_modules/mocha/bin/_mocha test/node/* test/node/models/**/*  --recursive
  ;;
  stg)
    export NODE_ENV=stg
    nodemon bin/www
  ;;
  qa)
    export NODE_ENV=qa
    nodemon bin/www
  ;;
  dev)
    mongod &
    redis-server &
    export NODE_ENV=development
    nodemon bin/www
  ;;
  *)
    echo "Usage: {test-api|jshint|coverage|stg|qa|dev}"
    exit 1
  ;;
esac

```

Esse meu arquivo **start.sh**, possui alguns truquezinhos como:

-> Identificar se está rodando num Mac ou num Linux, para exportar o caminho certo até o instantclient do Oracle (desenvolvo em Mac, mas o Jenkins e as máquinas de produção, QA e Stage são Linux).

-> Receber um argumento para executar o job correto, que podem ser: **test-api, jshint, coverage, stg, qa, dev**, ou qualquer outra coisa que for a sua necessidade.

A maior vantagem aqui, foi evitar aquela repetição de código no json, e simplificar essas execuções e a manutenção, ao delegar para um arquivo externo a responsabilidade de saber como executar cada uma das tarefas.

Lembre-se de dar permissão de execução para esse arquivo:

``` shell
$ chmod +x scripts/start.sh
```

E depois, melhore a legibilidade do teu package, apenas invocando o arquivo shell:

``` json
"scripts": {
  "start": "./scripts/start.sh dev",
  "qa": "./scripts/start.sh qa",
  "stg": "./scripts/start.sh stg",

  "pretest-coverage": "./scripts/start.sh jshint",
  "test-coverage": "./scripts/start.sh coverage",
  "test": "npm run test-coverage",

  "pretest-api": "jshint test/api/*",
  "test-api": "./scripts/start.sh test-api"
},
```

``` shell
$ npm start
$ npm run qa
$ npm run stg
$ npm run test-coverage
$ npm test
$ npm run test-api

```

Muito mais sucinto e limpo, ne?!

E ai, o que achou ? já usava isso ? comece agora!

## links interessantes:

http://substack.net/task\_automation\_with\_npm\_run
