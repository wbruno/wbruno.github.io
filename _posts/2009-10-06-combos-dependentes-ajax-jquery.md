---
id: 20
title: Combos dependentes AJAX-jQuery
date: 2009-10-06T00:35:41+00:00
author: William Bruno
excerpt: |
  Boas galera!
  Fiz aqui um exemplo do que eu mesmo já procurei muito por ai.
layout: post
guid: http://www.wbruno.com.br/blog/?p=20
permalink: /ajax/combos-dependentes-ajax-jquery/
dsq_thread_id:
  - "2101341484"
categories:
  - AJAX
---
Boas galera!

Fiz aqui um exemplo do que eu mesmo já procurei muito por ai.
  
Sou péssimo para explicações, então lá vão os códigos.

Embaixo no script php, eu comentei as linhas caso queria usar a biblioteca **mysql**, em vez da **mysqli**(prefira o **i**, caso MySQL > 4.1)
  
**index.php**

``` html
<html>
<head>
  <script type="text/javascript" src="jquery-1.3.2.min.js"></script>
  <script type="text/javascript">
  $(document).ready(function(){//inicio o jQuery
    $("select[name='combo1']").change(function(){
    var idCombo1 = $(this).val();//pegando o value do option selecionado
    //alert(idCombo1);//apenas para debugar a variável
    
      $.getJSON(//esse método do jQuery, só envia GET
        'combos-dependentes-function.inc.php',//script server-side que deverá retornar um objeto jSON
        {idCombo1: idCombo1},//enviando a variável

        function(data){
        //alert(data);//apenas para debugar a variável
          
          var option = new Array();//resetando a variável
          
          resetaCombo('combo2');//resetando o combo
          $.each(data, function(i, obj){
            
            
            option[i] = document.createElement('option');//criando o option
            $( option[i] ).attr( {value : obj.id} );//colocando o value no option
            $( option[i] ).append( obj.nome );//colocando o 'label'

            $("select[name='combo2']").append( option[i] );//jogando um à um os options no próximo combo
        });
      });
    });
  });  
  
  /* função pronta para ser reaproveitada, caso queria adicionar mais combos dependentes */
  function resetaCombo( el )
  {
    $("select[name='"+el+"']").empty();//retira os elementos antigos
    var option = document.createElement('option');          
    $( option ).attr( {value : '0'} );
    $( option ).append( 'Escolha' );
    $("select[name='"+el+"']").append( option );
  }
  </script>
</head>
<body>
<form action="" method="post">
  <fieldset>
    <label><select name="combo1">
      <option value="0">Escolha</option>

      <option value="1">Item 1</option>
      <option value="2">Item 2</option>
      <option value="3">Item 3</option>
    </select></label>
    
    <label><select name="combo2">
      <option value="0">Escolha</option>
    </select></label>

  </fieldset>
</form>
</body>
</html>
```

**combos-dependentes-function.inc.php**

``` php
<?php
  header("Content-Type: text/html; charset=ISO-8859-1");

  function intGet( $campo ){
    return isset( $_GET[$campo] ) ? (int)$_GET[$campo] : 0;
  }  
  function retorno( $id )
  {
    $sql = "SELECT `id`, `nome` 
      FROM `combo2` 
      WHERE `idCombo1` = {$id} ";
    $sql .= "ORDER BY `nome` ";
    
    
    $mysqli = new mysqli("localhost", "root", "123", "wbruno");

    
    $q = $mysqli->query( $sql ); 
    
    
    $json = Array();
    if( $q->num_rows > 0 )
    {
      while( $dados = $q->fetch_object() )
      {
        $json[]  = Array('nome'=> utf8_encode( $dados->nome ), 'id'=> $dados->id);
      }
    }
    else
      $json[]  = Array('nome'=> utf8_encode( 'nao encontrado' ), 'id'=> '0' );
      

    
    return json_encode( $json );
  }
  
  echo retorno( intGet('idCombo1') );

```

Uma forma simples de debugar, é acessando diretamente:
  
<a style="color: #284b72;" title="Link externo" href="http://www.wbruno.com.br/scripts/combos-dependentes-function.inc.php?idCombo1=1" rel="nofollow external">http://www.wbruno.com.br/scripts/combos-dependentes-function.inc.php?idCombo1=1</a>

No meu caso, fiz essa pasta &#8216;combo&#8217;, só para organizar as coisas por aqui.