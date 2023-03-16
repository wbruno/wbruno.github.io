---
id: 8
title: Classe php, retorna dia, mês e ano por extenso
date: 2009-08-16T23:47:15+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=8
permalink: /php/classe-php-retorna-dia-mes-e-ano-por-extenso/
dsq_thread_id:
  - "2101000255"
categories:
  - PHP
tags:
  - oo
---
eaee!!

Ainda brincando de wordpress.. como dormi o dia inteiro hoje, resolvi postar no iMasters.. vamos lá.. apenas &#8216;melhorando&#8217; uma classe que foi postada, cheguei no seguinte:

Créditos ao criador do tópico tb:

[http://forum.imasters.uol.com.br/index.php?/topic/358281-classe-para-retornar-a-data-por-extenso/page\_\_gopid\_\_1361894&#entry1361894](http://forum.imasters.uol.com.br/index.php?/topic/358281-classe-para-retornar-a-data-por-extenso/page__gopid__1361894&#entry1361894)

``` php
<?php
Class Data
{
        private $dia;
        private $diaSemana;
        private $mes;
        private $ano;

        /*
         * construtor
         */
        public function Data( $day='' )
        {
                if( $day == '' )
                {
                        $this->diaSemana = date('w');
                        $this->dia = date('d');
                        $this->mes = date('n');
                        $this->ano = date('Y');
                }
                else
                {
                        $p = explode('/', $day);
                        $this->dia = $p[];
                        $this->mes = $p[1];
                        $this->ano = $p[2];

                        $this->diaSemana = date("w", mktime(, , , $this->mes, $this->dia, $this->ano));
                }
        }
        public function getData( $string = 'Bauru' )
        {
                $mes = self::Mes();
                $diaSemana = self::Dia();
                $data = $string.', '.$diaSemana.' '.$this->dia.' de '.$mes.' de '.$this->ano;
                return $data;
        }

        public function Mes()
        {
                $Mes = array(
                1=>'Janeiro',
                2=>'Fevereiro',
                3=>'Março',
                4=>'Abril',
                5=>'Maio',
                6=>'Junho',
                7=>'Julho',
                8=>'Agosto',
                9=>'Setembro',
                10=>'Outubro',
                11=>'Novembro',
                12=>'Dezembro'
                );

                return $Mes[$this->mes];
        }

        public function Dia()
        {
                $Dia = array(
                =>'Domingo',
                1=>'Segunda-feira',
                2=>'Terça-feira',
                3=>'Quarta-feira',
                4=>'Quinta-feira',
                5=>'Sexta-feira',
                6=>'Sábado'
                );

                return $Dia[$this->diaSemana];
        }
}

/* para retornar uma data específica por extenso */
$Data = new Data('14/12/1988');//dia em que nasci ^^
echo $Data->getData();

echo '<hr />';

/* para retornar a data atual */
$Data = new Data();
echo $Data->getData();
?>
```