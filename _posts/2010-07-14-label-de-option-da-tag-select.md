---
id: 50
title: Label de Option da tag select
date: 2010-07-14T11:45:46+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=50
permalink: /javascript-puro/label-de-option-da-tag-select/
dsq_thread_id:
  - "2105228084"
categories:
  - Javascript
---
<pre name="code" class="html">&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
function label_option( el )
{
        var label = el.options[ el.selectedIndex ].text;
        alert( label );
}
window.onload = function()
{
        document.getElementById( 'teste' ).onchange = function()
        {
                label_option( this );
        }
}
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
        &lt;form action="" method="post"&gt;
        &lt;label&gt;Teste: &lt;select name="teste" id="teste"&gt;
                        &lt;option value=""&gt;--&lt;/option&gt;
                        &lt;option value="1"&gt;Um&lt;/option&gt;
                        &lt;option value="2"&gt;Dois&lt;/option&gt;
                        &lt;option value="3"&gt;Tres&lt;/option&gt;
                &lt;/select&gt;&lt;/label&gt;
        &lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

referência:
  
<a title="Link externo" rel="nofollow external" href="http://www.mredkj.com/tutorials/tutorial002.html">http://www.mredkj.co&#8230;utorial002.html</a>