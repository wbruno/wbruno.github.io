---
id: 14
title: Demonstração função setInterval Javascript
date: 2009-08-26T20:08:40+00:00
author: William Bruno
excerpt: Demostração de set interval
layout: post
guid: http://www.wbruno.com.br/blog/?p=14
permalink: /javascript-puro/demonstracao-funcao-setinterval-javascript/
categories:
  - Javascript
---
Dá uma olhada..
  
a cada 1 segundo e meio, vai aparecer um alert na tela.. e incrementar um contador&#8230;

<pre style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; margin-left: 10px; background-image: initial; background-repeat: initial; background-attachment: initial; -webkit-background-clip: initial; -webkit-background-origin: initial; background-color: #f8f8f8; overflow-x: auto; overflow-y: auto; font-size: 11px; line-height: 15px; background-position: initial initial; padding: 5px; border: 1px solid #c9c9c9;"><span style="color: #000088;">&lt;html&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;head&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;title&gt;</span><span style="color: #000000;">setInterval</span><span style="color: #000088;">&lt;/title&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;script</span><span style="color: #000000;"> </span><span style="color: #660066;">type</span><span style="color: #666600;">=</span><span style="color: #008800;">"text/javascript"</span><span style="color: #000088;">&gt;</span><span style="color: #000000;">
        </span><span style="color: #000088;">var</span><span style="color: #000000;"> i </span><span style="color: #666600;">=</span><span style="color: #000000;"> </span><span style="color: #006666;"></span><span style="color: #666600;">;</span><span style="color: #000000;">
        window</span><span style="color: #666600;">.</span><span style="color: #000000;">onload </span><span style="color: #666600;">=</span><span style="color: #000000;"> </span><span style="color: #000088;">function</span><span style="color: #666600;">()</span><span style="color: #000000;">
        </span><span style="color: #666600;">{</span><span style="color: #000000;">
                window</span><span style="color: #666600;">.</span><span style="color: #000000;">setInterval</span><span style="color: #666600;">(</span><span style="color: #000000;">ver</span><span style="color: #666600;">,</span><span style="color: #000000;"> </span><span style="color: #006666;">1500</span><span style="color: #666600;">);</span><span style="color: #000000;">
        </span><span style="color: #666600;">}</span><span style="color: #000000;">
        </span><span style="color: #000088;">function</span><span style="color: #000000;"> ver</span><span style="color: #666600;">()</span><span style="color: #000000;">
        </span><span style="color: #666600;">{</span><span style="color: #000000;">
                i</span><span style="color: #666600;">++;</span><span style="color: #000000;">
                </span><span style="color: #000088;">return</span><span style="color: #000000;"> alert</span><span style="color: #666600;">(</span><span style="color: #008800;">'Chamou: '</span><span style="color: #666600;">+</span><span style="color: #000000;">i</span><span style="color: #666600;">);</span><span style="color: #000000;">
        </span><span style="color: #666600;">}</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;/script&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;/head&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;body&gt;</span><span style="color: #000000;">

</span><span style="color: #000088;">&lt;/body&gt;</span><span style="color: #000000;">
</span><span style="color: #000088;">&lt;/html&gt;</span></pre>