---
id: 20
title: Alterar um a atributo privado fora da classe com reflection (PHP)
date: 2015-06-12T16:31:14+00:00
author: douglasjam
layout: post
guid: http://douglasjam.com.br/?p=20
permalink: http://douglasjam.com.br/2015/06/12/alterar-um-a-atributo-privado-com-reflection-php/
categories:
  - PHP
---
O exemplo abaixo mostra como é possível alterar uma propriedade mesmo que privada em tempo de execução com reflexão. Isto nos faz ficar um pouco mais alerta ao disponibilizar API&#8217;s e confiar que a mesma será restrita ao nosso escopo de classe.

<pre class="lang:php decode:true   ">&lt;?php

class Usuario {

private $nome = 'Douglas';

public function getNome(){
return $this-&gt;nome;
}

}

$teste = new Usuario();

// verificando que o valor é Douglas
echo $teste-&gt;getNome() . PHP_EOL;

// Tenta alterar o valor diretamente, lançará exception
//$teste-&gt;nome = 'Rodrigo';

// Faz a alteração em tempo de execução via reflection
$refObject = new ReflectionObject($teste);
$refProperty = $refObject-&gt;getProperty('nome');
$refProperty-&gt;setAccessible(true);
$refProperty-&gt;setValue($teste, 'Rodrigo');

// Confere que o valor foi realmente alterado em tempo de execução
echo $teste-&gt;getNome() . PHP_EOL;

//Confirmando que foi em execução e não afetou a classe
$teste2 = new Usuario();

echo $teste2-&gt;getNome() . PHP_EOL;</pre>

Saída:

<pre class="lang:default decode:true ">Douglas Rodrigo Douglas</pre>

&nbsp;