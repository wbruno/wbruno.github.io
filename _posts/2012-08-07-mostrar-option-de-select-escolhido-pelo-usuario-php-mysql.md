---
id: 2198
title: 'Mostrar option de select escolhido pelo usuário &#8211; php &#038; mysql'
date: 2012-08-07T10:51:48+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2198
permalink: /php/mostrar-option-de-select-escolhido-pelo-usuario-php-mysql/
dsq_thread_id:
  - "2100763550"
categories:
  - PHP
---
Boas!

Galera tem perguntando muito sobre isso no fórum.imasters.
  
Resolvi deixar aqui no meu blog, um pequeno script que faz essa rotina.

Deixar <var>selected</var>, um dos options de uma tag select, apartir do que o usuário escolheu antes, e já temos salvo no nosso banco de dados.

Primeiro declaro uma função, para evitar duplicação de código.

``` php
<?php
function selected( $value, $selected ){
    return $value==$selected ? ' selected="selected"' : '';
}
```

E então uso ela em cada um dos meus options:

``` html
<select name="te">
    <option value="">Escolha</option>
    <option value="masculino"<?php echo selected( 'masculino', $sexo ); ?>>Masculino</option>
    <option value="feminino"<?php echo selected( 'feminino', $sexo ); ?>>Feminino</option>
</select>
```

É isso galera.
  
Com essa simples rotina, conseguimos deixar marcado (selected=&#8221;selected&#8221;), a opção que o usuário tinha escolhido anteriormente.

Lembrando que a variavel <var>$sexo</var>, pode vir do mysql, ou de um $_POST de um passo anterior desse formulário.. enfim&#8230; tanto faz.