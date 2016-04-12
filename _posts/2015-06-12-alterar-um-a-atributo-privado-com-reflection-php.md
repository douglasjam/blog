---
layout: page
title: Alterar um a atributo privado fora da classe com reflection (PHP)
categories:
  - PHP
---
O exemplo abaixo mostra como é possível alterar uma propriedade mesmo que privada em tempo de execução com reflexão. Isto nos faz ficar um pouco mais alerta ao disponibilizar API&#8217;s e confiar que a mesma será restrita ao nosso escopo de classe.

{% highlight php %}
<?php

class Usuario {

private $nome = 'Douglas';

public function getNome(){
return $this-->nome;
}

}

$teste = new Usuario();

// verificando que o valor é Douglas
echo $teste-->getNome() . PHP_EOL;

// Tenta alterar o valor diretamente, lançará exception
//$teste-->nome = 'Rodrigo';

// Faz a alteração em tempo de execução via reflection
$refObject = new ReflectionObject($teste);
$refProperty = $refObject-->getProperty('nome');
$refProperty-->setAccessible(true);
$refProperty-->setValue($teste, 'Rodrigo');

// Confere que o valor foi realmente alterado em tempo de execução
echo $teste-->getNome() . PHP_EOL;

//Confirmando que foi em execução e não afetou a classe
$teste2 = new Usuario();

echo $teste2-->getNome() . PHP_EOL;
{% endhighlight %}

Saída:

{% highlight default %}
Douglas Rodrigo Douglas
{% endhighlight %}
