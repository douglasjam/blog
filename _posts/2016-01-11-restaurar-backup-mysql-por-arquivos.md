---
layout: post
title: Restaurar backup mysql por arquivos
category: Banco de Dados
tags: [banco-de-dados, linux, mysql, restaurar, backup, portugues]
---
Caso algum dia você não possa utilizar o mysqldump para fazer o backup corretamente e isolado do seu banco de dados mysql, seja por algum crash, alguma atualização ou modificação mal feita no servidor, você pode em ultimo caso recorrer ao backup manual dos arquivos, podendo assim você logo apos restaurar os arquivo em uma nova configuração de mysql.

Vou detalhar abaixo o passo a passo o qual segui para recuperar um banco apos este crash, no meu caso, apos um update do mysql para um versão superior, não conseguia mais ligar meu banco de dados mysql, e neste caso achei mais fácil retornar a versão anterior.<!--more-->Passo a passo:

1- Faça backup dos bancos de dados:

{% highlight bash %}
cp -rf /var/lib/mysql/ ~/backup_mysql
{% endhighlight %}
<!--more-->
2 &#8211; Reconfigure seu novo servidor

3 &#8211; Pare o servidor

{% highlight bash %}
service mysql stop
{% endhighlight %}

4 &#8211; Copie de volta os bancos de dados que deseja, normalmente estes sao separados por pastas

{% highlight bash %}
cp -rf ~/mysql_backup/meu_db /var/lib/mysql/
{% endhighlight %}

5 &#8211; Caso voce possua algum banco de dados InnoDB, voce tambem tera que copiar a pasta ibdata1.

{% highlight bash %}
cp -rf ~/mysql_backup/ibdata1 /var/lib/mysql/
{% endhighlight %}

6 &#8211; Restaure as permissoes dos arquivos

{% highlight bash %}
chown mysql:mysql /var/lib/mysql/* -R
{% endhighlight %}

7 &#8211; Reinicie o servidor, e provavelmente estará tudo funcionando

{% highlight bash %}
service mysql start
{% endhighlight %}
