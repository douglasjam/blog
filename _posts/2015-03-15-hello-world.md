---
id: 1
title: Criar Link Simbólico
date: 2015-03-15T14:21:05+00:00
author: douglasjam
layout: post
guid: http://douglasjam.com.br/?p=1
permalink: http://douglasjam.com.br/2015/03/15/hello-world/
dsq_thread_id:
  - 4502939532
categories:
  - Cloud
  - Linux
  - Windows
---
Para quem utiliza algum serviço de armazenamento nas nuvens, seja Dropbox, Google Drive, Skydrive ou afins, sempre se deparou com a questão que eles impõem, somente será sincronizado o que estiver na pasta X. Porém as vezes a gente se depara com a situação que o diretório que queremos fazer um backup nas nuvens talvez possa não ficar dentro da pasta que eles querem, como por exemplo, se você quiser fazer backup de algum arquivo/pasta que está em rede, ou dentro da pasta de algum programa especifico, ou acessar dentro do apache um diretorio fora do atual, ou seja um savegame no &#8220;C:/&#8230;&#8221; ou diretório de trabalho o qualquer outra coisa.

<!--more-->Para isso existe um truque chamado link simbólico, existente tanto em windows como em linux, que aparentemente é um atalho, mas é uma referência. Se você tentar colocar o atalho para backup no serviço Cloud não irá funcionar, pois apenas o atalho criado será sincronizado e não seu conteudo, mas se usar uma referência irá funcionar como desejado, é como se a pasta inteira estivesse lá dentro, pois a partir do momento que se cria a referência/link simbólico existirá dois caminhos para acessar o mesmo arquivo em disco.

Segue os comandos para criação do link simbolico em windows ou linux/debian.

&#8220;Uma nota, no Windows, para criar uma referência de alguma pasta na rede, opte por utilizar um mapeamento da unidade antes, é mais confiável&#8221;

**Windows**

<pre class="lang:default decode:true">mklink /D "C:/Arquivos de Programas/Jogo/Savegame" "C:/Users/XPTO/Dropbox"</pre>

**Linux/Debian**

<pre class="lang:default decode:true ">junction ln -s /var/www/sitea/files /var/www/siteb/sitea_files</pre>