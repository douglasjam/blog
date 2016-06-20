---
layout: post
title: Paginas estáticas com Jekyll
category: Uteis
figure: resources/img/jekyll.png
tags: [jekyll, blog, ruby, paginas estaticas]
---
Depois de alguns anos apenas utilizando Wordpress como principal sistema de blog ou CMS acabo conhecendo o [Jekyll](https://jekyllrb.com). Ele basicamente e um gerador de sites estáticos escrito em ruby que converte textos com marcações markdown, html, includes de partials e outras coisas providas por plugins em paginas estáticas html.

Ele permite que você faça quase tudo que um site escrito em PHP, C# ou Java, com a vantagem que após compilado, o resultado e apenas html, o que reduz os requisitos do servidor para basicamente um servidor de arquivos, já que o html e processado pelos navegadores.

Outro grande ponto e que, há varias empresas oferecendo hospedagem e ate compilação gratuita para ele, como por exemplo o [github pages](https://pages.github.com/), gitlab pages.

Este blog por exemplo, esta escrito nele, porem utilizo meu próprio servidor para hospeda-lo. Caso queira ver como estou desenvolvendo, pode conferir em [meu repositorio no github](github.com/douglasjam/blog).
<!--more-->

Segue abaixo alguns dos exemplos de uso do Jekyll que estou fazendo em meu blog, alem destes você pode encontrar diversos outros [plugins](https://jekyllrb.com/docs/plugins/) prontos para uso , alem de [temas](http://jekyllthemes.org/) como criar seus próprios plugins.

_Como nao consegui escapar o codigo jekyll, as tags de abertura/fechamento podem estao diferentes, porem normalmente e { % para interpretacao e { { para impressao._

- Definição de variáveis em paginas

{% highlight ruby %}
    ---
    layout: post
    title: Restaurar backup mysql por arquivos
    category: Banco de Dados
    tags: [banco-de-dados, linux, mysql, restaurar, backup]
    ---
    
    Conteudo do post ou pagina aqui...
{% endhighlight %}

- Iteracao entre valores de um array

{% highlight ruby %}
   % for tag in page.tags %
        <span class="label label-default">{ tag }</span>
    % endfor %
    
    % for post in paginator.posts %
        <h2><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h2>
    % endfor %
{% endhighlight %}

- Impressão de variáveis e formatação da saída

{% highlight ruby %}
    <span class="post-writed pull-left">
      Escrito em { page.date | date: " %d/%m/%Y" }
    </span>
{% endhighlight %}
    
- Inclusão de views
    
{% highlight ruby %}
    include layout-analytics.html
{% endhighlight %}

- Plugin para encapsular formatação de código fonte

{% highlight ruby %}
    % highlight bash %
        mklink /D "C:/Arquivos de Programas/Jogo/Savegame" "C:/Users/XPTO/Dropbox"
    % endhighlight %
{% endhighlight %}

- Plugin para transformar a imagem em thumbnail

{% highlight ruby %}
    % picture thumb_index resources/img/guerraespadas.jpg alt="Guerra das Espadas na Bahia" %
{% endhighlight %}

