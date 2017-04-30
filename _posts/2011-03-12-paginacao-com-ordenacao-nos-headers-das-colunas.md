---
id: 218
title: Paginação Com Ordenação Nos Headers Das Colunas
date: 2011-03-12T00:37:56+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=218
permalink: /sql/paginacao-com-ordenacao-nos-headers-das-colunas/
categories:
  - SQL
---
<a href="http://www.wbruno.com.br/scripts/paginacao-ordenacao-headers.php" target="_blank">Demostração</a>

<pre name="code" class="php">&lt;?php

        $con = mysql_connect('localhost', 'root', '123');
        mysql_select_db( 'price', $con );
       
        $sql = "SELECT `id`, `letra` FROM `alfabeto`";
        $query = mysql_query( $sql )or die( mysql_error() );
       
       
        $in = getGet('in') ? getGet('in') : 0;
       
       
        $por_pagina = 5;
        $inicio = $in*$por_pagina;
       
        $order = getGet('by') ? ' ORDER BY '.getGet('by').' '.getGet('order') : '';
        $sql = "SELECT `id`, `letra` FROM `alfabeto` {$order} LIMIT {$inicio}, {$por_pagina}";
        $query_paginada  = mysql_query( $sql )or die( mysql_error() );
       
       
        $total = mysql_num_rows( $query );
        echo 'Existem '.$total.' letras cadastradas! ';
        echo '&lt;table&gt;
                &lt;thead&gt;
                        &lt;tr&gt;
                                &lt;th&gt;&lt;a href="?in='.$in.'&order=asc&by=id"&gt;ID&lt;/a&gt;&lt;/th&gt;
                                &lt;th&gt;&lt;a href="?in='.$in.'&order=asc&by=letra"&gt;Letra&lt;/a&gt;&lt;/th&gt;
                        &lt;/tr&gt;
                &lt;/thead&gt;
                &lt;tbody&gt;
        ';
        while( $dados = mysql_fetch_assoc( $query_paginada ) )
        {
                echo '&lt;tr&gt;&lt;td&gt;'.$dados['id'].'&lt;/td&gt;&lt;td&gt;'.$dados['letra'].'&lt;/td&gt;&lt;/tr&gt;';
        }
        echo '&lt;/tbody&gt;&lt;/table&gt;';
       
        $order = getGet('by') ? '&order='.getGet('order').'&by='.getGet('by') : '';
        for( $i=0, $paginas=$total/$por_pagina; $i&lt;$paginas; $i++ )
                echo '&lt;a href="?in='.$i.$order.'"&gt;'.$i.'&lt;/a&gt; - ';
       
       
function getGet( $key ){
        return isset( $_GET[ $key ] ) ? $_GET[ $key ] : null;
}</pre>

estrutura

<pre name="code" class="sql">--
-- Estrutura da tabela `alfabeto`
--

CREATE TABLE IF NOT EXISTS `alfabeto` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `letra` char(1) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=14 ;

--
-- Extraindo dados da tabela `alfabeto`
--

INSERT INTO `alfabeto` (`id`, `letra`) VALUES
(1, 'a'),
(2, 'w'),
(3, 's'),
(4, 'd'),
(5, 'x'),
(6, 'f'),
(7, 't'),
(8, 'h'),
(9, 'i'),
(10, 'j'),
(11, 'k'),
(12, 'l'),
(13, 'z');</pre>