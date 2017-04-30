---
id: 2940
title: 'Escrevendo um javascript testável &#8211; Jasmine primeiros passos'
date: 2013-04-15T07:00:16+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2940
permalink: /javascript-puro/escrevendo-um-javascript-testavel-jasmine-primeiros-passos/
dsq_thread_id:
  - "2106267925"
categories:
  - Javascript
---
## Código de qualidade

Um dos passos para se escrever um código de qualidade, é escrever um código testável, e então os testes dele.

Ter rotinas automáticas que executem testes em nossos scripts também vai nos ajudar a refatorar certos trechos, com a garantia de que não quebramos nenhum comportamento.

## Código confiável

Os testes devem ser capazes de reproduzir todas as entradas e saídas esperadas. Assim, cada vez que vc mexer nele, não precisa se preocupar em testar manualmente todos os comportamentos. Pois vc pode esquecer de alguns, testar de forma errada outros.. enfim.. não é confiável.

Estamos acostumados a programar assim:

[<img src="http://wbruno.com.br/wp-content/uploads/2013/04/Captura-de-Tela-2013-04-11-às-10.47.44-288x300.png" alt="Código javascript não testável" width="288" height="300" class="aligncenter size-medium wp-image-2941" srcset="http://wbruno.com.br/wp-content/uploads/2013/04/Captura-de-Tela-2013-04-11-às-10.47.44-288x300.png 288w, http://wbruno.com.br/wp-content/uploads/2013/04/Captura-de-Tela-2013-04-11-às-10.47.44-984x1024.png 984w, http://wbruno.com.br/wp-content/uploads/2013/04/Captura-de-Tela-2013-04-11-às-10.47.44.png 990w" sizes="(max-width: 288px) 100vw, 288px" />](http://wbruno.com.br/wp-content/uploads/2013/04/Captura-de-Tela-2013-04-11-às-10.47.44.png)

Esse código acima, [formata um input em javascript com uma máscara assim: 000,0000](http://wbruno.com.br/2013/04/11/mascara-javascript-para-peso-com-preenchimento-ao-contrario/).
  
Ao preencher o primeiro número, o script formata para <var>0,0001</var>, e assim por diante, apagando os demais zeros.

Só que esse código não é testável, ou seja, escrever uma rotina que &#8220;use&#8221;, dando uma entrada e comparando se foi igual a uma saída esperada, não é algo trivial. Primeiro passo, é reescrever para conseguirmos chamar assim:
  
`formatWeight('123'); //0,0123`

## Evita duplicação de código

Note que não é preciso muito:

<pre class="javascript">&lt;script type="text/javascript">
function id(el){
    return document.getElementById(el);
}
function formatWeight(v){
	var integer = v.split(',')[0];

	v = v.replace(/\D/, "");
	v = v.replace(/^[0]+/, "");

	if(v.length &lt;= 4 || !integer)
	{
		if(v.length === 1) v = '0,000' + v;
		if(v.length === 2) v = '0,00' + v;
		if(v.length === 3) v = '0,0' + v;
		if(v.length === 4) v = '0,' + v;

	} else {
		v = v.replace(/^(\d{1,})(\d{4})$/, "$1,$2");
	}

	return v;
}
window.onload = function(){
	id('peso').onkeyup = function(){
		this.value = formatWeight(this.value);
	}
};
&lt;/script>
&lt;input type="text" name="peso" id="peso" maxlength="8" />
</pre>

E agora eu tenho um código isolado. E se eu precisar desse mesmo comportamento em outro input, posso apenas invocar:

<pre class="javascript">id('peso').onkeyup = function(){
		this.value = formatWeight(this.value);
	}
	id('peso2').onkeyup = function(){
		this.value = formatWeight(this.value);
	}</pre>

Evitando assim duplicar código.

Esse foi o primeiro ganho em ter me preocupado em escrever um código testável.

## Verificando a saída manualmente

Ainda não vou dizer como fazer com o Jasmine os testes, pois precisamos saber o que é um teste.
  
O script que propus aqui é super simples. São poucas possibilidades de entrada, e cada entrada gera um tipo de saída.

Fazendo na mão, eu escrevi todas as entradas possíveis, e olho na tela se o retorno foi o que eu queria.

<pre class="javascript">window.onload = function(){
	var $resultado = id('resultado'),
		p = '';

	p = formatWeight('1') + '&lt;br/>';
	p += formatWeight('12') + '&lt;br/>';
	p += formatWeight('123') + '&lt;br/>';
	p += formatWeight('1234') + '&lt;br/>';
	p += formatWeight('12345') + '&lt;br/>';
	p += formatWeight('123456') + '&lt;br/>';
	p += formatWeight('1234567') + '&lt;br/>';

	$resultado.innerHTML = p;
};
&lt;/script>

&lt;p id="resultado">&lt;/p></pre>

Isso já é &#8220;melhor&#8221; do que nada, e não preciso digitar mais 7 entradas diferentes no input, para ver se o resultado foi o certo. Testes durante o desenvolvimento são necessários. E fazer algo assim:

<pre class="javascript">id('resultado').innerHTML += 'Entrou: 1234567 e saiu: ' 
		+ formatWeight('1234567') + ', ' 
		+ (formatWeight('1234567') == '123,4567') + '&lt;br/>';
</pre>

É chato e pouco produtivo.

## Jasmine

[<img src="http://wbruno.com.br/wp-content/uploads/2013/04/jasmine_logo.png" alt="jasmine_logo" width="282" height="90" class="aligncenter size-full wp-image-2942" />](http://wbruno.com.br/wp-content/uploads/2013/04/jasmine_logo.png)

1. Baixe o <a href="https://github.com/pivotal/jasmine/downloads" rel="nofollow"><strong>jasmine standalone</strong></a>.

2. Copie a pasta lib e o arquivo SpecRunner.html, pode colar eles dentro de um diretório **tests**, do teu projeto, ou algo assim.

3. Edite as seguintes linhas do SpecRunner:

<pre class="javascript">&lt;!-- include source files here... -->
  &lt;script type="text/javascript" src="src/Player.js">&lt;/script>
  &lt;script type="text/javascript" src="src/Song.js">&lt;/script>

  &lt;!-- include spec files here... -->
  &lt;script type="text/javascript" src="spec/SpecHelper.js">&lt;/script>
  &lt;script type="text/javascript" src="spec/PlayerSpec.js">&lt;/script></pre>

No meu caso ficaram assim:

<pre class="javascript">&lt;!-- include source files here... -->
  &lt;script type="text/javascript" src="formatWeight.js">&lt;/script>

  &lt;!-- include spec files here... -->
  &lt;script type="text/javascript" src="spec/formatWeightSpec.js">&lt;/script></pre>

O arquivo **formatWeigth.js**, contém apenas a função formatWeight(), e a função id().
  
A chamada do window.onload, está lá no meu projeto. E o arquivo **formatWeigtSpec.js** é o teste em si. A entrada e a saída esperada.

4. Vamos ver o formatWeigtSpec.js:

<pre class="javascript">describe("formatWeight", function() {


	it("should be equal", function() {
		expect(formatWeight('1')).toEqual('0,0001');
	});

});
</pre>

5. Pronto! testes feitos. Podemos até refatorar o código, com a certeza de que nenhum comportamento vai ser quebrado, e nem precisar ficar digitando no input toda hora para ver se o script faz oque deveria.

Meu código final de testes ficou assim:

<pre class="javascript">describe("formatWeight", function() {

	var arrIn = [
		'1', '12', '123', '1234', '12345', '123456', '1234567', 'abc', 'a1b2c3'
	],
	arrOut = [
		'0,0001', '0,0012', '0,0123', '0,1234', '1,2345', '12,3456', '123,4567', '0,0000', '0,0123'
	],
	i,
	arrInLength = arrIn.length;


	for(i = 0; i&lt;arrInLength; i++) {

		(function(entry, output_expected){

			it( entry + " should be equal " + output_expected, function() {
				expect(formatWeight(entry)).toEqual(output_expected);
			});

		}(arrIn[i], arrOut[i]));
	}

});</pre>

Com segurança, posso refatorar a parte do código que me incomodava.

Chegando assim ao meu código final:

<pre class="javascript">function id(el){
    return document.getElementById(el);
}
function formatWeight(v){
	var integer = v.split(',')[0],
		zeroFill = 0,
		c = '';

	v = v.replace(/\D/g, "");
	v = v.replace(/^[0]+/, "");

	if(v.length &lt;= 4 || !integer)
	{
		zeroFill = 4 - v.length;
		while(zeroFill--) {
			c += '0';
		}
		v = '0,' + c + v;

	} else {
		v = v.replace(/^(\d{1,})(\d{4})$/, "$1,$2");
	}

	return v;
}</pre>

Agora vc é capaz de usar o Jasmine como framework para testes. Comente com a sua experiência.
  
Ficou em dúvida ? Quer ver como ficou tudo junto ? Baixa lá no meu git:

<a href="https://github.com/wbruno/formatWeight" rel="nofollow">https://github.com/wbruno/formatWeight</a>