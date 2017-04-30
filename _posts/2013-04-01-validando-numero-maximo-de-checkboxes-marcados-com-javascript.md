---
id: 2937
title: Validando número máximo de checkboxes marcados com javascript
date: 2013-04-01T15:35:53+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2937
permalink: /javascript-puro/validando-numero-maximo-de-checkboxes-marcados-com-javascript/
dsq_thread_id:
  - "2102862857"
categories:
  - Javascript
---
Post simples hoje. Em um grupo com 4 checkboxes, o usuário pode marcar no máximo 2, e em um grupo de 6 checkboxes ele pode marcar no máximo 3.

Note que ao dar um f5 no browser, o mesmo mantém os valores já respondidos em um formulário. Por isso eu faço uma contagem inicial sempre que a página carrega, verificando quantos checkboxes já estão marcados.

## Código HTML

<pre name="code" class="javascript">&lt;!DOCTYPE HTML>
&lt;html lang="en-US">
&lt;head>
    &lt;meta charset="UTF-8">
    &lt;title>Validando número maximo de checkboxes marcados&lt;/title>
    &lt;style type="text/css">
	label { display: block; }
	.error { color: #f00; }
    &lt;/style>
&lt;/head>
&lt;body>
&lt;article>

    &lt;h1>Perguntas&lt;/h1>

    &lt;form action="app.php" method="post" id="form-app">
 
        &lt;fieldset id="field1">
            &lt;legend class="question">Quais?&lt;/legend>

            &lt;label>&lt;input type="checkbox" value="a" name="question[4][]"> a&lt;/label>
            &lt;label>&lt;input type="checkbox" value="b" name="question[4][]"> b&lt;/label>
            &lt;label>&lt;input type="checkbox" value="c" name="question[4][]"> c&lt;/label>
            &lt;label>&lt;input type="checkbox" value="d" name="question[4][]"> d&lt;/label>

            &lt;p class="error is-hidden" id="error1">Escolha no máximo 2 opções&lt;/p>
        &lt;/fieldset>

        &lt;fieldset id="field2">
            &lt;legend class="question">Quais?&lt;/legend>

            &lt;label>&lt;input type="checkbox" value="a" name="question[5][]"> a&lt;/label>
            &lt;label>&lt;input type="checkbox" value="b" name="question[5][]"> b&lt;/label>
            &lt;label>&lt;input type="checkbox" value="c" name="question[5][]"> c&lt;/label>
            &lt;label>&lt;input type="checkbox" value="d" name="question[5][]"> d&lt;/label>
            &lt;label>&lt;input type="checkbox" value="e" name="question[5][]"> e&lt;/label>
            &lt;label>&lt;input type="checkbox" value="f" name="question[5][]"> f&lt;/label>


            &lt;p class="error is-hidden" id="error2">Escolha no máximo 3 opções&lt;/p>
        &lt;/fieldset>

        &lt;input class="btn" id="btn" type="submit" value="Enviar" name="enviar">
    &lt;/form>
&lt;/article>

&lt;script type="text/javascript" src="all.js">&lt;/script>
&lt;/body>
&lt;/html>
</pre>

## Código JavaScript

<pre name="code" class="javascript">(function () {
    'use strict';
    /*global document:false*/

    function byId(id) {
        return document.getElementById(id);
    }

    var $form = byId('form-app'),
        $btn = byId('btn'),

        field1 = {
            field : byId('field1'),
            checks : byId('field1').getElementsByTagName('input'),
            pError : byId('error1'),
            max: 2,
            qnt: 0,
            state: true
        },
        field2 = {
            field : byId('field2'),
            checks : byId('field2').getElementsByTagName('input'),
            pError : byId('error2'),
            max: 3,
            qnt: 0,
            state: true
        };

    function toggleButton() {
        var cb = function() {
            return false;
        };
        $btn.className = 'btn is-disabled';
        
        if (field1.state && field2.state) {
            $btn.className = 'btn';
            cb = function() {
                return true;
            };
        }

        $form.onsubmit = cb;
    }
    function verifyMax(field) {
        if (field.qnt > field.max) {
            field.pError.style.display = 'block';
            field.state = false;
        } else {
            field.pError.style.display = 'none';
            field.state = true;
        }
        toggleButton();
    }
    function countChoice(field) {
        var inputs = field.checks,
            qnt = 0,
            i = field.checks.length;

        while (i--) {
            qnt += inputs[i].checked;
        }
        field.qnt = qnt;

        verifyMax(field);
    }
    function maxChoice(field) {
        var i = field.checks.length;

        countChoice(field);

        while (i--) {
            field.checks[i].onclick = function() {
                field.qnt = this.checked ? field.qnt + 1 : field.qnt - 1;
                verifyMax(field);
            };
        }
    }

    maxChoice(field1);
    maxChoice(field2);

}());</pre>