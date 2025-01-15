---
id: 50
title: Label de Option da tag select
date: 2010-07-14T11:45:46+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=50
permalink: /javascript-puro/label-de-option-da-tag-select/
dsq_thread_id:
  - "2105228084"
categories:
  - Javascript
---
``` html
<html>
<head>
<script type="text/javascript">
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
</script>
</head>
<body>
        <form action="" method="post">
        <label>Teste: <select name="teste" id="teste">
                        <option value="">--</option>
                        <option value="1">Um</option>
                        <option value="2">Dois</option>
                        <option value="3">Tres</option>
                </select></label>
        </form>
</body>
</html>
```

referência:

<a title="Link externo" rel="nofollow external" href="http://www.mredkj.com/tutorials/tutorial002.html">http://www.mredkj.co&#8230;utorial002.html</a>
