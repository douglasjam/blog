---
id: 5
title: Renomear tabelas Mysql
date: 2015-03-15T14:41:00+00:00
author: douglasjam
layout: post
guid: http://douglasjam.com.br/?p=5
permalink: http://douglasjam.com.br/2015/03/15/renomear-tabelas-mysql/
categories:
  - Banco de Dados
  - Mysql
---
Pode acontecer de alguma vez você precisar fazer uma operação em lote em um banco seu, onde será necessário renomear todas as tabelas adicionando um prefixo, sufixo ou até alterar o nome delas, seja qual for o motivo, existe um método mais produtivo que renomear elas por alguma interface uma a uma que é por um script caso o número de tabelas seja grande. O script abaixo faz a leitura de todas as tabelas do banco e mediante esta leitura eu concateno algum comando de alteração do nome mais a consulta que troca o nome, segue o comando abaixo.

<pre class="lang:mysql decode:true ">SELECT concat('RENAME TABLE ', table_name, ' TO ', concat('ds_', table_name), ';')
FROM information_schema.tables
where table_schema like 'bancosistema'</pre>

Após executar esta query a saída será parecida com a abaixo, no caso solicitei a adição do sufixo &#8220;ds_&#8221; ao nome de cada tabela, após basta exportar da maneira que achar mais conveniente esta saída e executar o script que todas as tabelas serão renomeadas.

<pre class="lang:mysql decode:true ">RENAME TABLE contasprogramadas TO ds_contasprogramadas;
RENAME TABLE contratoguinchos TO ds_contratoguinchos;
RENAME TABLE empresas TO ds_empresas;
RENAME TABLE filiais TO ds_filiais;
</pre>