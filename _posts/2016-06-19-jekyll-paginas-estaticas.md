---
layout: post
title: Jekyll Paginas Estaticas
category: Linux
figure: resources/img/jekyll.jpg
tags: [jekyll, blog, ruby, paginas estaticas]
---------------------------------------------------------------------------------------------
 
Depois de alguns anos apenas utilizando Wordpress como principal sistema de blog ou CMS acabo conhecendo o [Jekyll](https://jekyllrb.com). Ele basicamente e um gerador de sites estáticos escrito em ruby que converte textos com marcações markdown, html, includes de partials e outras coisas providas por plugins em paginas estáticas html.

Ele permite que você faça quase tudo que um site escrito em PHP, C# ou Java, com a vantagem que após compilado, o resultado e apenas html, o que reduz os requisitos do servidor para basicamente um servidor de arquivos, já que o html e processado pelos navegadores.

Outro grande ponto e que, há varias empresas oferecendo hospedagem e ate compilação gratuita para ele, como por exemplo o [github pages](https://pages.github.com/), gitlab pages.

Este blog por exemplo, esta escrito nele, porem utilizo meu próprio servidor para hospeda-lo. Caso queira ver como estou desenvolvendo, pode conferir em [meu repositorio no github](github.com/douglasjam/blog).

Segue abaixo alguns dos exemplos de uso do Jekyll que estou fazendo em meu blog, alem destes você pode encontrar diversos outros [plugins](https://jekyllrb.com/docs/plugins/) prontos para uso , alem de [temas](http://jekyllthemes.org/) como criar seus próprios plugins.

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
    \u007b\u0025 for tag in page.tags \u0025\u007d
        <span class="label label-default">{{ tag }}</span>
    \u007b\u0025 endfor \u0025\u007d
    
    \u007b\u0025 for post in paginator.posts \u0025\u007d
        <h2><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h2>
    \u007b\u0025 endfor \u0025\u007d
{% endhighlight %}

- Impressão de variáveis e formatação da saída

{% highlight ruby %}
    <span class="post-writed pull-left">
      Escrito em \u007b\u007b page.date | date: " %d/%m/%Y" \u007d\u007d
    </span>
{% endhighlight %}
    
- Inclusão de views
    
{% highlight ruby %}
    \u007b\u0025 include layout-analytics.html \u0025\u007d
{% endhighlight %}

- Plugin para encapsular formatação de código fonte

{% highlight ruby %}
    \u007b\u007b\u0025 highlight bash \u0025\u007d
        mklink /D "C:/Arquivos de Programas/Jogo/Savegame" "C:/Users/XPTO/Dropbox"
    \u007b\u0025 endhighlight \u0025\u007d
{% endhighlight %}

- Plugin para transformar a imagem em thumbnail

{% highlight ruby %}
    \u007b\u0025 picture thumb_index resources/img/guerraespadas.jpg alt="Guerra das Espadas na Bahia" \u0025\u007d
{% endhighlight %}

