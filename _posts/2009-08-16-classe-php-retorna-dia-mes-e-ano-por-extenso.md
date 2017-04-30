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

<pre style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; margin-left: 10px; background-image: initial; background-repeat: initial; background-attachment: initial; -webkit-background-clip: initial; -webkit-background-origin: initial; background-color: #f8f8f8; overflow-x: auto; overflow-y: auto; font-size: 11px; line-height: 12px; background-position: initial initial; padding: 5px; border: 1px solid #c9c9c9;"><span style="color: #666600;">&lt;?</span><span style="color: #000000;">php
</span><span style="color: #660066;">Class</span><span style="color: #000000;"> </span><span style="color: #660066;">Data</span><span style="color: #000000;">
</span><span style="color: #666600;">{</span><span style="color: #000000;">
        </span><span style="color: #000088;">private</span><span style="color: #000000;"> $dia</span><span style="color: #666600;">;</span><span style="color: #000000;">
        </span><span style="color: #000088;">private</span><span style="color: #000000;"> $diaSemana</span><span style="color: #666600;">;</span><span style="color: #000000;">
        </span><span style="color: #000088;">private</span><span style="color: #000000;"> $mes</span><span style="color: #666600;">;</span><span style="color: #000000;">
        </span><span style="color: #000088;">private</span><span style="color: #000000;"> $ano</span><span style="color: #666600;">;</span><span style="color: #000000;">

        </span><span style="color: #880000;">/*
         * construtor
         */</span><span style="color: #000000;">
        </span><span style="color: #000088;">public</span><span style="color: #000000;"> </span><span style="color: #000088;">function</span><span style="color: #000000;"> </span><span style="color: #660066;">Data</span><span style="color: #666600;">(</span><span style="color: #000000;"> $day</span><span style="color: #666600;">=</span><span style="color: #008800;">''</span><span style="color: #000000;"> </span><span style="color: #666600;">)</span><span style="color: #000000;">
        </span><span style="color: #666600;">{</span><span style="color: #000000;">
                </span><span style="color: #000088;">if</span><span style="color: #666600;">(</span><span style="color: #000000;"> $day </span><span style="color: #666600;">==</span><span style="color: #000000;"> </span><span style="color: #008800;">''</span><span style="color: #000000;"> </span><span style="color: #666600;">)</span><span style="color: #000000;">
                </span><span style="color: #666600;">{</span><span style="color: #000000;">
                        $this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">diaSemana </span><span style="color: #666600;">=</span><span style="color: #000000;"> date</span><span style="color: #666600;">(</span><span style="color: #008800;">'w'</span><span style="color: #666600;">);</span><span style="color: #000000;">
                        $this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">dia </span><span style="color: #666600;">=</span><span style="color: #000000;"> date</span><span style="color: #666600;">(</span><span style="color: #008800;">'d'</span><span style="color: #666600;">);</span><span style="color: #000000;">
                        $this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">mes </span><span style="color: #666600;">=</span><span style="color: #000000;"> date</span><span style="color: #666600;">(</span><span style="color: #008800;">'n'</span><span style="color: #666600;">);</span><span style="color: #000000;">
                        $this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">ano </span><span style="color: #666600;">=</span><span style="color: #000000;"> date</span><span style="color: #666600;">(</span><span style="color: #008800;">'Y'</span><span style="color: #666600;">);</span><span style="color: #000000;">
                </span><span style="color: #666600;">}</span><span style="color: #000000;">
                </span><span style="color: #000088;">else</span><span style="color: #000000;">
                </span><span style="color: #666600;">{</span><span style="color: #000000;">
                        $p </span><span style="color: #666600;">=</span><span style="color: #000000;"> explode</span><span style="color: #666600;">(</span><span style="color: #008800;">'/'</span><span style="color: #666600;">,</span><span style="color: #000000;"> $day</span><span style="color: #666600;">);</span><span style="color: #000000;">
                        $this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">dia </span><span style="color: #666600;">=</span><span style="color: #000000;"> $p</span><span style="color: #666600;">[</span><span style="color: #006666;"></span><span style="color: #666600;">];</span><span style="color: #000000;">
                        $this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">mes </span><span style="color: #666600;">=</span><span style="color: #000000;"> $p</span><span style="color: #666600;">[</span><span style="color: #006666;">1</span><span style="color: #666600;">];</span><span style="color: #000000;">
                        $this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">ano </span><span style="color: #666600;">=</span><span style="color: #000000;"> $p</span><span style="color: #666600;">[</span><span style="color: #006666;">2</span><span style="color: #666600;">];</span><span style="color: #000000;">

                        $this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">diaSemana </span><span style="color: #666600;">=</span><span style="color: #000000;"> date</span><span style="color: #666600;">(</span><span style="color: #008800;">"w"</span><span style="color: #666600;">,</span><span style="color: #000000;"> mktime</span><span style="color: #666600;">(</span><span style="color: #006666;"></span><span style="color: #666600;">,</span><span style="color: #000000;"> </span><span style="color: #006666;"></span><span style="color: #666600;">,</span><span style="color: #000000;"> </span><span style="color: #006666;"></span><span style="color: #666600;">,</span><span style="color: #000000;"> $this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">mes</span><span style="color: #666600;">,</span><span style="color: #000000;"> $this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">dia</span><span style="color: #666600;">,</span><span style="color: #000000;"> $this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">ano</span><span style="color: #666600;">));</span><span style="color: #000000;">
                </span><span style="color: #666600;">}</span><span style="color: #000000;">
        </span><span style="color: #666600;">}</span><span style="color: #000000;">
        </span><span style="color: #000088;">public</span><span style="color: #000000;"> </span><span style="color: #000088;">function</span><span style="color: #000000;"> getData</span><span style="color: #666600;">(</span><span style="color: #000000;"> $string </span><span style="color: #666600;">=</span><span style="color: #000000;"> </span><span style="color: #008800;">'Bauru'</span><span style="color: #000000;"> </span><span style="color: #666600;">)</span><span style="color: #000000;">
        </span><span style="color: #666600;">{</span><span style="color: #000000;">
                $mes </span><span style="color: #666600;">=</span><span style="color: #000000;"> </span><span style="color: #000088;">self</span><span style="color: #666600;">::</span><span style="color: #660066;">Mes</span><span style="color: #666600;">();</span><span style="color: #000000;">
                $diaSemana </span><span style="color: #666600;">=</span><span style="color: #000000;"> </span><span style="color: #000088;">self</span><span style="color: #666600;">::</span><span style="color: #660066;">Dia</span><span style="color: #666600;">();</span><span style="color: #000000;">
                $data </span><span style="color: #666600;">=</span><span style="color: #000000;"> $string</span><span style="color: #666600;">.</span><span style="color: #008800;">', '</span><span style="color: #666600;">.</span><span style="color: #000000;">$diaSemana</span><span style="color: #666600;">.</span><span style="color: #008800;">' '</span><span style="color: #666600;">.</span><span style="color: #000000;">$this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">dia</span><span style="color: #666600;">.</span><span style="color: #008800;">' de '</span><span style="color: #666600;">.</span><span style="color: #000000;">$mes</span><span style="color: #666600;">.</span><span style="color: #008800;">' de '</span><span style="color: #666600;">.</span><span style="color: #000000;">$this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">ano</span><span style="color: #666600;">;</span><span style="color: #000000;">
                </span><span style="color: #000088;">return</span><span style="color: #000000;"> $data</span><span style="color: #666600;">;</span><span style="color: #000000;">
        </span><span style="color: #666600;">}</span><span style="color: #000000;">

        </span><span style="color: #000088;">public</span><span style="color: #000000;"> </span><span style="color: #000088;">function</span><span style="color: #000000;"> </span><span style="color: #660066;">Mes</span><span style="color: #666600;">()</span><span style="color: #000000;">
        </span><span style="color: #666600;">{</span><span style="color: #000000;">
                $Mes </span><span style="color: #666600;">=</span><span style="color: #000000;"> array</span><span style="color: #666600;">(</span><span style="color: #000000;">
                </span><span style="color: #006666;">1</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Janeiro'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">2</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Fevereiro'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">3</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Março'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">4</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Abril'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">5</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Maio'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">6</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Junho'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">7</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Julho'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">8</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Agosto'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">9</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Setembro'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">10</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Outubro'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">11</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Novembro'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">12</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Dezembro'</span><span style="color: #000000;">
                </span><span style="color: #666600;">);</span><span style="color: #000000;">

                </span><span style="color: #000088;">return</span><span style="color: #000000;"> $Mes</span><span style="color: #666600;">[</span><span style="color: #000000;">$this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">mes</span><span style="color: #666600;">];</span><span style="color: #000000;">
        </span><span style="color: #666600;">}</span><span style="color: #000000;">

        </span><span style="color: #000088;">public</span><span style="color: #000000;"> </span><span style="color: #000088;">function</span><span style="color: #000000;"> </span><span style="color: #660066;">Dia</span><span style="color: #666600;">()</span><span style="color: #000000;">
        </span><span style="color: #666600;">{</span><span style="color: #000000;">
                $Dia </span><span style="color: #666600;">=</span><span style="color: #000000;"> array</span><span style="color: #666600;">(</span><span style="color: #000000;">
                </span><span style="color: #006666;"></span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Domingo'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">1</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Segunda-feira'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">2</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Terça-feira'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">3</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Quarta-feira'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">4</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Quinta-feira'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">5</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Sexta-feira'</span><span style="color: #666600;">,</span><span style="color: #000000;">
                </span><span style="color: #006666;">6</span><span style="color: #666600;">=&gt;</span><span style="color: #008800;">'Sábado'</span><span style="color: #000000;">
                </span><span style="color: #666600;">);</span><span style="color: #000000;">

                </span><span style="color: #000088;">return</span><span style="color: #000000;"> $Dia</span><span style="color: #666600;">[</span><span style="color: #000000;">$this</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">diaSemana</span><span style="color: #666600;">];</span><span style="color: #000000;">
        </span><span style="color: #666600;">}</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">

</span><span style="color: #880000;">/* para retornar uma data específica por extenso */</span><span style="color: #000000;">
$Data </span><span style="color: #666600;">=</span><span style="color: #000000;"> </span><span style="color: #000088;">new</span><span style="color: #000000;"> </span><span style="color: #660066;">Data</span><span style="color: #666600;">(</span><span style="color: #008800;">'14/12/1988'</span><span style="color: #666600;">);</span><span style="color: #880000;">//dia em que nasci ^^</span><span style="color: #000000;">
echo $Data</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">getData</span><span style="color: #666600;">();</span><span style="color: #000000;">

echo </span><span style="color: #008800;">'&lt;hr /&gt;'</span><span style="color: #666600;">;</span><span style="color: #000000;">

</span><span style="color: #880000;">/* para retornar a data atual */</span><span style="color: #000000;">
$Data </span><span style="color: #666600;">=</span><span style="color: #000000;"> </span><span style="color: #000088;">new</span><span style="color: #000000;"> </span><span style="color: #660066;">Data</span><span style="color: #666600;">();</span><span style="color: #000000;">
echo $Data</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">getData</span><span style="color: #666600;">();</span><span style="color: #000000;">
</span><span style="color: #666600;">?&gt;</span></pre>