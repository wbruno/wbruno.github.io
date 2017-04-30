---
id: 24
title: 'Suggest AJAX &#8211; jQuery &#8211; php/Mysql'
date: 2010-01-08T23:32:31+00:00
author: William Bruno
excerpt: Resolvi brincar um pouquinho aqui..
layout: post
guid: http://www.wbruno.com.br/blog/?p=24
permalink: /ajax/suggest-ajax-jquery-phpmysql/
dsq_thread_id:
  - "2101473987"
categories:
  - AJAX
---
Resolvi brincar um pouquinho aqui..

<pre style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; margin-left: 10px; background-image: initial; background-repeat: initial; background-attachment: initial; -webkit-background-clip: initial; -webkit-background-origin: initial; background-color: #f8f8f8; overflow-x: auto; overflow-y: auto; font-size: 11px; line-height: 15px; background-position: initial initial; padding: 5px; border: 1px solid #c9c9c9;"><span style="color: #000088;">&lt;html&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;head&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;title&gt;</span><span style="color: #000000;">Suggest</span><span style="color: #000088;">&lt;/title&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;style</span><span style="color: #000000;"> </span><span style="color: #660066;">type</span><span style="color: #666600;">=</span><span style="color: #008800;">"text/css"</span><span style="color: #000088;">&gt;</span><span style="color: #000000;">
</span><span style="color: #666600;">*</span><span style="color: #000000;"> </span><span style="color: #666600;">{</span><span style="color: #000000;">
        margin</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;"></span><span style="color: #666600;">;</span><span style="color: #000000;">
        padding</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;"></span><span style="color: #666600;">;</span><span style="color: #000000;">
        list</span><span style="color: #666600;">-</span><span style="color: #000000;">style</span><span style="color: #666600;">:</span><span style="color: #000000;"> none</span><span style="color: #666600;">;</span><span style="color: #000000;">
        border</span><span style="color: #666600;">:</span><span style="color: #000000;"> none</span><span style="color: #666600;">;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">
form </span><span style="color: #666600;">{</span><span style="color: #000000;">
        width</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;">400px</span><span style="color: #666600;">;</span><span style="color: #000000;">
        margin</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;"></span><span style="color: #000000;"> </span><span style="color: #000088;">auto</span><span style="color: #666600;">;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">
form label </span><span style="color: #666600;">{</span><span style="color: #000000;">
        display</span><span style="color: #666600;">:</span><span style="color: #000000;"> block</span><span style="color: #666600;">;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">
form label input </span><span style="color: #666600;">{</span><span style="color: #000000;">
        margin</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;">2px</span><span style="color: #666600;">;</span><span style="color: #000000;">
        padding</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;">2px</span><span style="color: #666600;">;</span><span style="color: #000000;">
        border</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;">1px</span><span style="color: #000000;"> solid </span><span style="color: #880000;">#000;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">
</span><span style="color: #666600;">.</span><span style="color: #000000;">suggest </span><span style="color: #666600;">{</span><span style="color: #000000;">
        position</span><span style="color: #666600;">:</span><span style="color: #000000;"> relative</span><span style="color: #666600;">;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">
</span><span style="color: #666600;">.</span><span style="color: #000000;">suggest input </span><span style="color: #666600;">{</span><span style="color: #000000;">
        width</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;">250px</span><span style="color: #666600;">;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">
</span><span style="color: #880000;">#suggest {</span><span style="color: #000000;">
        position</span><span style="color: #666600;">:</span><span style="color: #000000;"> absolute</span><span style="color: #666600;">;</span><span style="color: #000000;">
        top</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;">22px</span><span style="color: #666600;">;</span><span style="color: #000000;">
        right</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;">64px</span><span style="color: #666600;">;</span><span style="color: #000000;">
        background</span><span style="color: #666600;">-</span><span style="color: #000000;">color</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #880000;">#fff;</span><span style="color: #000000;">
        width</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;">248px</span><span style="color: #666600;">;</span><span style="color: #000000;">
        text</span><span style="color: #666600;">-</span><span style="color: #000000;">align</span><span style="color: #666600;">:</span><span style="color: #000000;"> left</span><span style="color: #666600;">;</span><span style="color: #000000;">
        border</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;">1px</span><span style="color: #000000;"> solid </span><span style="color: #880000;">#000;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">
</span><span style="color: #880000;">#suggest li {</span><span style="color: #000000;">
        margin</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #006666;">2px</span><span style="color: #666600;">;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">
</span><span style="color: #880000;">#suggest a {</span><span style="color: #000000;">
        display</span><span style="color: #666600;">:</span><span style="color: #000000;"> block</span><span style="color: #666600;">;</span><span style="color: #000000;">
        color</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #880000;">#000;</span><span style="color: #000000;">
        text</span><span style="color: #666600;">-</span><span style="color: #000000;">decoration</span><span style="color: #666600;">:</span><span style="color: #000000;"> none</span><span style="color: #666600;">;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">
</span><span style="color: #880000;">#suggest a:hover {</span><span style="color: #000000;">
        background</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #880000;">#eee;</span><span style="color: #000000;">
        text</span><span style="color: #666600;">-</span><span style="color: #000000;">decoration</span><span style="color: #666600;">:</span><span style="color: #000000;"> underline</span><span style="color: #666600;">;</span><span style="color: #000000;">
        color</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #880000;">#f00;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">

</span><span style="color: #000088;">&lt;/style&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;script</span><span style="color: #000000;"> </span><span style="color: #660066;">type</span><span style="color: #666600;">=</span><span style="color: #008800;">"text/javascript"</span><span style="color: #000000;"> </span><span style="color: #660066;">src</span><span style="color: #666600;">=</span><span style="color: #008800;">"jquery.js"</span><span style="color: #000088;">&gt;</span><span style="color: #666600;">&lt;</span><span style="color: #008800;">/script&gt;
&lt;script type="text/</span><span style="color: #000000;">javascript</span><span style="color: #008800;">"&gt;</span><span style="color: #000000;">
        $</span><span style="color: #666600;">(</span><span style="color: #000000;">document</span><span style="color: #666600;">).</span><span style="color: #000000;">ready</span><span style="color: #666600;">(</span><span style="color: #000088;">function</span><span style="color: #666600;">(){</span><span style="color: #000000;">
                $</span><span style="color: #666600;">(</span><span style="color: #008800;">"input[name='suggest']"</span><span style="color: #666600;">).</span><span style="color: #000000;">keyup</span><span style="color: #666600;">(</span><span style="color: #000088;">function</span><span style="color: #666600;">(){</span><span style="color: #000000;">
                        createList</span><span style="color: #666600;">(</span><span style="color: #008800;">'.suggest'</span><span style="color: #666600;">);</span><span style="color: #000000;">
                        $</span><span style="color: #666600;">.</span><span style="color: #000000;">ajax</span><span style="color: #666600;">({</span><span style="color: #000000;">
                                type</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #008800;">"GET"</span><span style="color: #666600;">,</span><span style="color: #880000;">//apenas pra ficar mais fácil de debugar, pode mudar para POST depois</span><span style="color: #000000;">
                                url</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #008800;">"function.php"</span><span style="color: #666600;">,</span><span style="color: #000000;">
                                data</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #008800;">"parte="</span><span style="color: #666600;">+</span><span style="color: #000000;">$</span><span style="color: #666600;">(</span><span style="color: #000088;">this</span><span style="color: #666600;">).</span><span style="color: #000000;">val</span><span style="color: #666600;">(),</span><span style="color: #000000;">
                                success</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #000088;">function</span><span style="color: #666600;">(</span><span style="color: #000000;"> data </span><span style="color: #666600;">){</span><span style="color: #000000;">
                                        $</span><span style="color: #666600;">(</span><span style="color: #008800;">"#suggest"</span><span style="color: #666600;">).</span><span style="color: #000000;">html</span><span style="color: #666600;">(</span><span style="color: #000000;"> data </span><span style="color: #666600;">);</span><span style="color: #000000;">
                                </span><span style="color: #666600;">}</span><span style="color: #000000;">
                        </span><span style="color: #666600;">});</span><span style="color: #000000;">
                </span><span style="color: #666600;">});</span><span style="color: #000000;">

                $</span><span style="color: #666600;">(</span><span style="color: #008800;">"#suggest a"</span><span style="color: #666600;">).</span><span style="color: #000000;">live</span><span style="color: #666600;">(</span><span style="color: #008800;">'click'</span><span style="color: #666600;">,</span><span style="color: #000000;"> </span><span style="color: #000088;">function</span><span style="color: #666600;">(</span><span style="color: #000000;"> e </span><span style="color: #666600;">){</span><span style="color: #000000;">
                        e</span><span style="color: #666600;">.</span><span style="color: #000000;">preventDefault</span><span style="color: #666600;">();</span><span style="color: #000000;">
                        </span><span style="color: #000088;">var</span><span style="color: #000000;"> href </span><span style="color: #666600;">=</span><span style="color: #000000;"> $</span><span style="color: #666600;">(</span><span style="color: #000088;">this</span><span style="color: #666600;">).</span><span style="color: #000000;">attr</span><span style="color: #666600;">(</span><span style="color: #008800;">'href'</span><span style="color: #666600;">);</span><span style="color: #000000;">
                        </span><span style="color: #000088;">var</span><span style="color: #000000;"> id </span><span style="color: #666600;">=</span><span style="color: #000000;"> href</span><span style="color: #666600;">.</span><span style="color: #000000;">split</span><span style="color: #666600;">(</span><span style="color: #008800;">'='</span><span style="color: #666600;">);</span><span style="color: #000000;">

                        $</span><span style="color: #666600;">(</span><span style="color: #008800;">"input[name='id']"</span><span style="color: #666600;">).</span><span style="color: #000000;">val</span><span style="color: #666600;">(</span><span style="color: #000000;"> id</span><span style="color: #666600;">[</span><span style="color: #006666;">1</span><span style="color: #666600;">]</span><span style="color: #000000;"> </span><span style="color: #666600;">);</span><span style="color: #000000;">
                        $</span><span style="color: #666600;">(</span><span style="color: #008800;">"input[name='nome']"</span><span style="color: #666600;">).</span><span style="color: #000000;">val</span><span style="color: #666600;">(</span><span style="color: #000000;"> $</span><span style="color: #666600;">(</span><span style="color: #000088;">this</span><span style="color: #666600;">).</span><span style="color: #000000;">text</span><span style="color: #666600;">()</span><span style="color: #000000;"> </span><span style="color: #666600;">);</span><span style="color: #000000;">

                        $</span><span style="color: #666600;">(</span><span style="color: #008800;">"#suggest"</span><span style="color: #666600;">).</span><span style="color: #000000;">remove</span><span style="color: #666600;">();</span><span style="color: #000000;">
                </span><span style="color: #666600;">});</span><span style="color: #000000;">
                $</span><span style="color: #666600;">(</span><span style="color: #008800;">"#suggest"</span><span style="color: #666600;">).</span><span style="color: #000000;">mouseout</span><span style="color: #666600;">(</span><span style="color: #000088;">function</span><span style="color: #666600;">(){</span><span style="color: #000000;">
                        $</span><span style="color: #666600;">(</span><span style="color: #008800;">"#suggest"</span><span style="color: #666600;">).</span><span style="color: #000000;">remove</span><span style="color: #666600;">();</span><span style="color: #000000;">
                </span><span style="color: #666600;">});</span><span style="color: #000000;">
        </span><span style="color: #666600;">});</span><span style="color: #000000;">
        </span><span style="color: #000088;">function</span><span style="color: #000000;"> createList</span><span style="color: #666600;">(</span><span style="color: #000000;"> el </span><span style="color: #666600;">)</span><span style="color: #000000;">
        </span><span style="color: #666600;">{</span><span style="color: #000000;">
                $</span><span style="color: #666600;">(</span><span style="color: #008800;">"#suggest"</span><span style="color: #666600;">).</span><span style="color: #000000;">remove</span><span style="color: #666600;">();</span><span style="color: #000000;">

                </span><span style="color: #000088;">var</span><span style="color: #000000;"> list </span><span style="color: #666600;">=</span><span style="color: #000000;"> document</span><span style="color: #666600;">.</span><span style="color: #000000;">createElement</span><span style="color: #666600;">(</span><span style="color: #008800;">'ul'</span><span style="color: #666600;">);</span><span style="color: #000000;">
                list</span><span style="color: #666600;">.</span><span style="color: #000000;">id </span><span style="color: #666600;">=</span><span style="color: #000000;"> </span><span style="color: #008800;">'suggest'</span><span style="color: #666600;">;</span><span style="color: #000000;">
                $</span><span style="color: #666600;">(</span><span style="color: #000000;"> el </span><span style="color: #666600;">).</span><span style="color: #000000;">append</span><span style="color: #666600;">(</span><span style="color: #000000;"> list </span><span style="color: #666600;">);</span><span style="color: #000000;">
        </span><span style="color: #666600;">}</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;/script&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;/head&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;body&gt;</span><span style="color: #000000;">
        </span><span style="color: #000088;">&lt;form</span><span style="color: #000000;"> </span><span style="color: #660066;">action</span><span style="color: #666600;">=</span><span style="color: #008800;">""</span><span style="color: #000000;"> </span><span style="color: #660066;">method</span><span style="color: #666600;">=</span><span style="color: #008800;">"post"</span><span style="color: #000088;">&gt;</span><span style="color: #000000;">
                </span><span style="color: #000088;">&lt;fieldset&gt;</span><span style="color: #000000;">
                        </span><span style="color: #000088;">&lt;label</span><span style="color: #000000;"> </span><span style="color: #660066;">class</span><span style="color: #666600;">=</span><span style="color: #008800;">"suggest"</span><span style="color: #000088;">&gt;</span><span style="color: #000000;">Vá digitando: </span><span style="color: #000088;">&lt;input</span><span style="color: #000000;"> </span><span style="color: #660066;">type</span><span style="color: #666600;">=</span><span style="color: #008800;">"text"</span><span style="color: #000000;"> </span><span style="color: #660066;">name</span><span style="color: #666600;">=</span><span style="color: #008800;">"suggest"</span><span style="color: #000000;"> </span><span style="color: #000088;">/&gt;&lt;/label&gt;</span><span style="color: #000000;">

                        </span><span style="color: #000088;">&lt;label&gt;</span><span style="color: #000000;">ID: </span><span style="color: #000088;">&lt;input</span><span style="color: #000000;"> </span><span style="color: #660066;">type</span><span style="color: #666600;">=</span><span style="color: #008800;">"text"</span><span style="color: #000000;"> </span><span style="color: #660066;">name</span><span style="color: #666600;">=</span><span style="color: #008800;">"id"</span><span style="color: #000000;"> </span><span style="color: #000088;">/&gt;&lt;/label&gt;</span><span style="color: #000000;">
                        </span><span style="color: #000088;">&lt;label&gt;</span><span style="color: #000000;">Nome: </span><span style="color: #000088;">&lt;input</span><span style="color: #000000;"> </span><span style="color: #660066;">type</span><span style="color: #666600;">=</span><span style="color: #008800;">"text"</span><span style="color: #000000;"> </span><span style="color: #660066;">name</span><span style="color: #666600;">=</span><span style="color: #008800;">"nome"</span><span style="color: #000000;"> </span><span style="color: #000088;">/&gt;&lt;/label&gt;</span><span style="color: #000000;">
                </span><span style="color: #000088;">&lt;/fieldset&gt;</span><span style="color: #000000;">
        </span><span style="color: #000088;">&lt;/form&gt;</span><span style="color: #000000;">
        </span><span style="color: #000088;">&lt;p&gt;</span><span style="color: #000000;">Procure por: William, B, J..</span><span style="color: #000088;">&lt;/p&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;/body&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;/html&gt;</span></pre>

e o sql disso:

<pre style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; margin-left: 10px; background-image: initial; background-repeat: initial; background-attachment: initial; -webkit-background-clip: initial; -webkit-background-origin: initial; background-color: #f8f8f8; overflow-x: auto; overflow-y: auto; font-size: 11px; line-height: 15px; background-position: initial initial; padding: 5px; border: 1px solid #c9c9c9;"><span style="color: #666600;">--</span><span style="color: #000000;">
</span><span style="color: #666600;">--</span><span style="color: #000000;"> </span><span style="color: #660066;">Banco</span><span style="color: #000000;"> de </span><span style="color: #660066;">Dados</span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #008800;">`ajax`</span><span style="color: #000000;">
</span><span style="color: #666600;">--</span><span style="color: #000000;">

</span><span style="color: #666600;">--</span><span style="color: #000000;"> </span><span style="color: #666600;">--------------------------------------------------------</span><span style="color: #000000;">

</span><span style="color: #666600;">--</span><span style="color: #000000;">
</span><span style="color: #666600;">--</span><span style="color: #000000;"> </span><span style="color: #660066;">Estrutura</span><span style="color: #000000;"> da tabela </span><span style="color: #008800;">`cliente`</span><span style="color: #000000;">
</span><span style="color: #666600;">--</span><span style="color: #000000;">

CREATE TABLE IF NOT EXISTS </span><span style="color: #008800;">`cliente`</span><span style="color: #000000;"> </span><span style="color: #666600;">(</span><span style="color: #000000;">
  </span><span style="color: #008800;">`id`</span><span style="color: #000000;"> </span><span style="color: #000088;">int</span><span style="color: #666600;">(</span><span style="color: #006666;">11</span><span style="color: #666600;">)</span><span style="color: #000000;"> </span><span style="color: #000088;">unsigned</span><span style="color: #000000;"> NOT NULL AUTO_INCREMENT</span><span style="color: #666600;">,</span><span style="color: #000000;">
  </span><span style="color: #008800;">`nome`</span><span style="color: #000000;"> varchar</span><span style="color: #666600;">(</span><span style="color: #006666;">50</span><span style="color: #666600;">)</span><span style="color: #000000;"> NOT NULL</span><span style="color: #666600;">,</span><span style="color: #000000;">
  PRIMARY KEY </span><span style="color: #666600;">(</span><span style="color: #008800;">`id`</span><span style="color: #666600;">),</span><span style="color: #000000;">
  KEY </span><span style="color: #008800;">`cliente_indexnome`</span><span style="color: #000000;"> </span><span style="color: #666600;">(</span><span style="color: #008800;">`nome`</span><span style="color: #666600;">)</span><span style="color: #000000;">
</span><span style="color: #666600;">)</span><span style="color: #000000;"> ENGINE</span><span style="color: #666600;">=</span><span style="color: #660066;">MyISAM</span><span style="color: #000000;">  DEFAULT CHARSET</span><span style="color: #666600;">=</span><span style="color: #000000;">latin1 PACK_KEYS</span><span style="color: #666600;">=</span><span style="color: #006666;"></span><span style="color: #000000;"> AUTO_INCREMENT</span><span style="color: #666600;">=</span><span style="color: #006666;">7</span><span style="color: #000000;"> </span><span style="color: #666600;">;</span><span style="color: #000000;">

</span><span style="color: #666600;">--</span><span style="color: #000000;">
</span><span style="color: #666600;">--</span><span style="color: #000000;"> </span><span style="color: #660066;">Extraindo</span><span style="color: #000000;"> dados da tabela </span><span style="color: #008800;">`cliente`</span><span style="color: #000000;">
</span><span style="color: #666600;">--</span><span style="color: #000000;">

INSERT INTO </span><span style="color: #008800;">`cliente`</span><span style="color: #000000;"> </span><span style="color: #666600;">(</span><span style="color: #008800;">`id`</span><span style="color: #666600;">,</span><span style="color: #000000;"> </span><span style="color: #008800;">`nome`</span><span style="color: #666600;">)</span><span style="color: #000000;"> VALUES
</span><span style="color: #666600;">(</span><span style="color: #006666;">1</span><span style="color: #666600;">,</span><span style="color: #000000;"> </span><span style="color: #008800;">'Jeovane Reges'</span><span style="color: #666600;">),</span><span style="color: #000000;">
</span><span style="color: #666600;">(</span><span style="color: #006666;">2</span><span style="color: #666600;">,</span><span style="color: #000000;"> </span><span style="color: #008800;">'Felipe Gonçalves'</span><span style="color: #666600;">),</span><span style="color: #000000;">
</span><span style="color: #666600;">(</span><span style="color: #006666;">3</span><span style="color: #666600;">,</span><span style="color: #000000;"> </span><span style="color: #008800;">'William'</span><span style="color: #666600;">),</span><span style="color: #000000;">
</span><span style="color: #666600;">(</span><span style="color: #006666;">4</span><span style="color: #666600;">,</span><span style="color: #000000;"> </span><span style="color: #008800;">'William Bruno'</span><span style="color: #666600;">),</span><span style="color: #000000;">
</span><span style="color: #666600;">(</span><span style="color: #006666;">5</span><span style="color: #666600;">,</span><span style="color: #000000;"> </span><span style="color: #008800;">'Bruno'</span><span style="color: #666600;">),</span><span style="color: #000000;">
</span><span style="color: #666600;">(</span><span style="color: #006666;">6</span><span style="color: #666600;">,</span><span style="color: #000000;"> </span><span style="color: #008800;">'Bruno Rocha'</span><span style="color: #666600;">);</span></pre>

<strong style="font-style: normal; font-weight: bold !important;">function.php</strong>

<pre style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; margin-left: 10px; background-image: initial; background-repeat: initial; background-attachment: initial; -webkit-background-clip: initial; -webkit-background-origin: initial; background-color: #f8f8f8; overflow-x: auto; overflow-y: auto; font-size: 11px; line-height: 15px; background-position: initial initial; padding: 5px; border: 1px solid #c9c9c9;"><span style="color: #666600;">&lt;?</span><span style="color: #000000;">php
        header</span><span style="color: #666600;">(</span><span style="color: #008800;">"Content-Type: text/html; charset=ISO-8859-1"</span><span style="color: #666600;">);</span><span style="color: #000000;">

        echo suggest</span><span style="color: #666600;">(</span><span style="color: #000000;"> getGet</span><span style="color: #666600;">(</span><span style="color: #008800;">'parte'</span><span style="color: #666600;">)</span><span style="color: #000000;"> </span><span style="color: #666600;">);</span><span style="color: #000000;">

</span><span style="color: #000088;">function</span><span style="color: #000000;"> suggest</span><span style="color: #666600;">(</span><span style="color: #000000;"> $palavra </span><span style="color: #666600;">)</span><span style="color: #000000;">
</span><span style="color: #666600;">{</span><span style="color: #000000;">
        $sql </span><span style="color: #666600;">=</span><span style="color: #000000;"> </span><span style="color: #008800;">"SELECT `id`, `nome` FROM `cliente` "</span><span style="color: #666600;">;</span><span style="color: #000000;">
        </span><span style="color: #000088;">if</span><span style="color: #666600;">(</span><span style="color: #000000;"> </span><span style="color: #666600;">!</span><span style="color: #000000;">empty</span><span style="color: #666600;">(</span><span style="color: #000000;">$palavra</span><span style="color: #666600;">)</span><span style="color: #000000;"> </span><span style="color: #666600;">)</span><span style="color: #000000;">
                $sql </span><span style="color: #666600;">.=</span><span style="color: #000000;"> </span><span style="color: #008800;">"WHERE `nome` LIKE '{$palavra}%'"</span><span style="color: #666600;">;</span><span style="color: #000000;">

        $mysqli </span><span style="color: #666600;">=</span><span style="color: #000000;"> </span><span style="color: #000088;">new</span><span style="color: #000000;"> mysqli</span><span style="color: #666600;">(</span><span style="color: #000000;"> </span><span style="color: #008800;">'localhost'</span><span style="color: #666600;">,</span><span style="color: #008800;">'root'</span><span style="color: #666600;">,</span><span style="color: #008800;">'123'</span><span style="color: #666600;">,</span><span style="color: #008800;">'ajax'</span><span style="color: #000000;"> </span><span style="color: #666600;">);</span><span style="color: #000000;">
        $query </span><span style="color: #666600;">=</span><span style="color: #000000;"> $mysqli</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">query</span><span style="color: #666600;">(</span><span style="color: #000000;"> $sql </span><span style="color: #666600;">);</span><span style="color: #000000;">
        </span><span style="color: #000088;">if</span><span style="color: #666600;">(</span><span style="color: #000000;"> $query</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">num_rows</span><span style="color: #666600;">&gt;</span><span style="color: #006666;"></span><span style="color: #000000;"> </span><span style="color: #666600;">)</span><span style="color: #000000;">
        </span><span style="color: #666600;">{</span><span style="color: #000000;">
                $li</span><span style="color: #666600;">=</span><span style="color: #008800;">''</span><span style="color: #666600;">;</span><span style="color: #000000;">
                </span><span style="color: #000088;">while</span><span style="color: #666600;">(</span><span style="color: #000000;"> $dados </span><span style="color: #666600;">=</span><span style="color: #000000;"> $query</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">fetch_object</span><span style="color: #666600;">()</span><span style="color: #000000;"> </span><span style="color: #666600;">)</span><span style="color: #000000;">
                        $li </span><span style="color: #666600;">.=</span><span style="color: #000000;"> </span><span style="color: #008800;">'&lt;li&gt;&lt;a href="?id='</span><span style="color: #666600;">.</span><span style="color: #000000;">$dados</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">id</span><span style="color: #666600;">.</span><span style="color: #008800;">'"&gt;'</span><span style="color: #666600;">.</span><span style="color: #000000;">$dados</span><span style="color: #666600;">-&gt;</span><span style="color: #000000;">nome</span><span style="color: #666600;">.</span><span style="color: #008800;">'&lt;/a&gt;&lt;/li&gt;'</span><span style="color: #666600;">;</span><span style="color: #000000;">
        </span><span style="color: #666600;">}</span><span style="color: #000000;">
        </span><span style="color: #000088;">else</span><span style="color: #000000;">
                $li </span><span style="color: #666600;">=</span><span style="color: #000000;"> </span><span style="color: #008800;">'Nenhum cadastro encontrado!'</span><span style="color: #666600;">;</span><span style="color: #000000;">

        </span><span style="color: #000088;">return</span><span style="color: #000000;"> $li</span><span style="color: #666600;">;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">
</span><span style="color: #000088;">function</span><span style="color: #000000;"> getGet</span><span style="color: #666600;">(</span><span style="color: #000000;"> $campo </span><span style="color: #666600;">){</span><span style="color: #000000;">
        </span><span style="color: #000088;">return</span><span style="color: #000000;"> </span><span style="color: #666600;">(</span><span style="color: #000000;"> isset</span><span style="color: #666600;">(</span><span style="color: #000000;">$_GET</span><span style="color: #666600;">[</span><span style="color: #000000;"> $campo </span><span style="color: #666600;">])</span><span style="color: #000000;"> </span><span style="color: #666600;">)</span><span style="color: #000000;"> </span><span style="color: #666600;">?</span><span style="color: #000000;"> filter</span><span style="color: #666600;">(</span><span style="color: #000000;"> $_GET</span><span style="color: #666600;">[</span><span style="color: #000000;"> $campo </span><span style="color: #666600;">]</span><span style="color: #000000;"> </span><span style="color: #666600;">)</span><span style="color: #000000;"> </span><span style="color: #666600;">:</span><span style="color: #000000;"> </span><span style="color: #000088;">null</span><span style="color: #666600;">;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span><span style="color: #000000;">
</span><span style="color: #000088;">function</span><span style="color: #000000;"> filter</span><span style="color: #666600;">(</span><span style="color: #000000;"> $var </span><span style="color: #666600;">)</span><span style="color: #000000;">
</span><span style="color: #666600;">{</span><span style="color: #000000;">
        </span><span style="color: #000088;">if</span><span style="color: #666600;">(</span><span style="color: #000000;"> </span><span style="color: #666600;">!</span><span style="color: #000000;">get_magic_quotes_gpc</span><span style="color: #666600;">()</span><span style="color: #000000;"> </span><span style="color: #666600;">)</span><span style="color: #000000;">
                $str </span><span style="color: #666600;">=</span><span style="color: #000000;"> mysql_real_escape_string</span><span style="color: #666600;">(</span><span style="color: #000000;"> $var </span><span style="color: #666600;">);</span><span style="color: #000000;">
        </span><span style="color: #000088;">else</span><span style="color: #000000;">
                $str </span><span style="color: #666600;">=</span><span style="color: #000000;"> $var</span><span style="color: #666600;">;</span><span style="color: #000000;">
        $str </span><span style="color: #666600;">=</span><span style="color: #000000;"> str_replace</span><span style="color: #666600;">(</span><span style="color: #000000;"> </span><span style="color: #008800;">'#'</span><span style="color: #666600;">,</span><span style="color: #000000;"> </span><span style="color: #008800;">'\#'</span><span style="color: #666600;">,</span><span style="color: #000000;"> $str </span><span style="color: #666600;">);</span><span style="color: #000000;">
        </span><span style="color: #000088;">return</span><span style="color: #000000;"> $str</span><span style="color: #666600;">;</span><span style="color: #000000;">
</span><span style="color: #666600;">}</span></pre>

<img style="vertical-align: middle; border: 0px initial initial;" src="http://forum.imasters.uol.com.br/public/style_emoticons/default/happy.gif" alt="^_^" />

Em funcionamento:
  
<a style="color: #284b72;" title="Link externo" rel="nofollow external" href="http://www.wbruno.com.br/scripts/suggest.php">http://www.wbruno.co&#8230;pts/suggest.php</a>
  
<img style="vertical-align: middle; border: 0px initial initial;" src="http://forum.imasters.uol.com.br/public/style_emoticons/default/natal_happy.gif" alt=":natal_happy:" />

em asp:
  
http://forum.imasters.com.br/index.php?/topic/403150-autocomplete-do-banco-de-dados