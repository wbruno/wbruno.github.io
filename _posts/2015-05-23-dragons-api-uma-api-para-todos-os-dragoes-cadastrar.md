---
id: 3384
title: 'Dragons API &#8211; Uma API para todos os dragões cadastrar'
date: 2015-05-23T21:49:07+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3384
permalink: /nodejs/dragons-api-uma-api-para-todos-os-dragoes-cadastrar/
videourl:
  - ""
categories:
  - NodeJS
---
[<img src="/wp-content/uploads/2015/05/dragons-api-1024x332.png" alt="dragons-api" width="788" height="255" class="aligncenter size-large wp-image-3385" srcset="/wp-content/uploads/2015/05/dragons-api-1024x332.png 1024w, /wp-content/uploads/2015/05/dragons-api-300x97.png 300w, /wp-content/uploads/2015/05/dragons-api-788x255.png 788w, /wp-content/uploads/2015/05/dragons-api.png 1458w" sizes="(max-width: 788px) 100vw, 788px" />](https://dragons-api.herokuapp.com)

O Express (<http://expressjs.com>) é um framework web, okay? Não seja &#8220;criativo&#8221; para inventar a sua própria estrutura maluca. Siga o que o framework diz, entenda a estrutura dele.

Se você quer fazer &#8220;do seu modo&#8221;, você está deixando de aproveitar as boas coisas do framework. Não reinvente a roda, quando ela já foi projetada e padronizada!

<!--more-->

O express generator (<http://expressjs.com/starter/generator.html>) é um pacote npm que cria uma estrutura inicial para um projeto express. Use.

Vou explicar cada um dos diretórios ou arquivos importantes para que você entenda como organizar uma aplicação NodeJS com Express.

<img src="/wp-content/uploads/2015/05/express-folder-1024x514.png" alt="express-folder" width="788" height="396" class="aligncenter size-large wp-image-3391" srcset="/wp-content/uploads/2015/05/express-folder-1024x514.png 1024w, /wp-content/uploads/2015/05/express-folder-300x151.png 300w, /wp-content/uploads/2015/05/express-folder-788x395.png 788w, /wp-content/uploads/2015/05/express-folder.png 1594w" sizes="(max-width: 788px) 100vw, 788px" />

## bin/www

Esse arquivo é criado pelo express-generator. Ele possui diversas boas práticas e deve sim ficar isolado do restante da configuração do express. É nele por exemplo, onde iremos mexer para escalar o node verticalmente, adicionando clusters.

## config

A pasta config é onde ficarão os arquivos de configuração, que não são nada mais do que os dados de conexão, urls de web services.. enfim, apenas informações ou endereços. Isso é uma config. Esses arquivos são burros, não possuem nenhuma lógica. Por isso, são arquivos **.json**

## controllers

A pasta controllers é onde colocamos o C do MVC. Um controller é responsável por **entender o que o usuário pediu, e retornar com alguma coisa**. Pronto.

## db

Frequentemente, temos que nos conectar com mais de um banco de dados. Nesse diretório, eu coloco um wrapper para os bancos de dados que vou utilizar. É onde fica o tratamento de erros caso o banco caia por exemplo. Esse também é o único ponto da aplicação que sabe usar a config de dados do banco para conectar com ele.

## models

O M do MVC. Um model é responsável por regras de negócio e por representar nossas entidades. Note que em NodeJS por questões de performance, não utilizaremos o pattern ActiveRecord. Eu prefiro muito mais o DAO (menos consumo de memória e maior simplicidade).

## public

São os arquivos estáticos: css, js e imagens. Essa pasta idealmente não é nem servida pelo NodeJS. O Nginx faz um trabalho melhor e consume menos memória para servir estáticos. Além disso, queremos o nosso NodeJS se preocupando em fazer outras coisas, e não essa tarefa trivial. Não queremos concorrer uma pesquisa no banco, com a entrega de um arquivo css. Esses arquivos não serão processados, por isso chamamos de estáticos.

## routes

Na pasta routes ficam a definição dos endpoints. Uma rota está associada a um método do controller. Pode parecer desnecessária essa divisão por enquanto, mas quando adicionarmos autenticação, regras de ACL, então o routes ficará com mais responsabilidades, e por isso é uma boa idéia separar.

## src

Aqui eu coloco os arquivos fonte do css e js que irei servir. Eu desenvolvo neles, o gulp roda e cria os arquivos \*.min.\* para mim.

## tests/unit

Coloco aqui os testes unitários. Aqueles em que eu tive que mockar o banco de dados. Dentro desse diretório iremos praticamente repetir a estrutura do projeto, com a pasta controllers, models&#8230; pois faremos testes arquivo por arquivo, função por função. Importante lembrar que um teste unitário não depende de nada, nem de banco e nem do teste anterior. Cada teste deve rodar isoladamente e não causar side effects em outro teste.

## tests/api

São testes &#8220;caixa preta&#8221;, onde eu finjo não conhecer exatamente a implementação. Bateremos diretamente na API, sem nos preocupar com cada método de cada arquivo, mas sim com cada rota e com o que ela pode fazer. Esses testes testam a integração da aplicação com as dependências dela. Então eles utilizam bancos de dados e tudo mais o que precisarem. Porém, a regra de que um teste não pode afetar outro continua valendo. Por isso limpamos o banco após cada teste.

## views

São os arquivos html do template. A camada de visualização que iremos apresentar para o usuário. Como esses arquivos serão processados pelo template engine, então eles não ficam dentro da public.

## app.js

O arquivo app.js é onde fica a configuração do Express. É assim que o express generator faz e é uma boa escolha continuarmos fazendo assim. Esse arquivo exporta o app, assim os testes podem utilizar o app sem o side effect do listener do servidor, por isso o separamos na bin/www.

Desenvolver com NodeJS não é só legal, é extremamente prazeroso. Veja os scripts que criei:

**package.json**

<pre>"scripts": {
    "start": "node ./bin/www",
    "pretest": "./node_modules/jshint/bin/jshint *.js models/*.js controllers/*.js tests/*",
    "test": "...",
    "test-api": "...",
    "nodemon": "export DEBUG=dragons:* && nodemon ./bin/www"
  },</pre>

Você executa eles com:

<pre>$ npm start
$ npm test # o pretest é executado antes do test. O npm sempre procura pelo sufixo pre antes de executar algum script.
$ npm run test-api
$ npm run nodemon</pre>

A API tem:

* documentação em html.

* healthcheck.

* mongoose.

* promise.

* crud completo.

* testes unitários (mock).

* testes funcionais (com banco).

Roadmap:

* melhorar o tratamento de erro.

* criar rotas para filtrar.

* cadastrar todos os dragões.

* terminar de modelar a entidade Dragão.

Pretendo cadastrar nessa API **todos** os dragões que existem por ai, me ajuda ?

Ainda não terminei a modelagem da entidade Dragão, então podemos discutir o que é legal de adicionar.

## API no Heroku

<https://dragons-api.herokuapp.com>.

## Github

<https://github.com/wbruno/dragons-api>.
