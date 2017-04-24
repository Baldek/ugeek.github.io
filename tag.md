---
layout: page
title: Etiquetas
description: Stochastic stuff blog's tags. List of articles and posts by tags.
---
# Secciones
Haz click sobre las secciones para acceder a los posts.
> * <a href="#seccion4">Listado de Etiquetas ordenadas alfabéticamente</a>
> * <a href="#seccion3">Listado de Posts clasificados por Etiquetas</a>


> * <a href="https://ugeek.github.io/tag2#podcast">Podcast</a>
> * <a href="https://ugeek.github.io/tag2#Blog">Blog</a>
> * <a href="https://ugeek.github.io/tag2#Blog">Podcast de Interes</a>
> * <a href="#seccion1">Escucha los Podcast en la web desde ivoox</a>
> * <a href="#seccion2">Twitter</a>


<a name="seccion4">Listado de Etiquetas ordenadas alfabéticamente</a>  

Haz click sobre el tag y verás el listado de posts.
<a href="#top">Volver al inicio</a>

<!-- Get the tag name for every tag on the site and set them
to the `site_tags` variable. -->
{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}

<!-- `tag_words` is a sorted array of the tag names. -->
{% assign tag_words = site_tags | split:',' | sort %}

<!-- Build the Page -->

<!-- List of all tags -->
<ul class="tags">
  {% for item in (0..site.tags.size) %}{% unless forloop.last %} {% capture this_word %}{{ tag_words[item] }}{% endcapture %}<a href="#{{ this_word | cgi_escape }}" class="tag">{{ this_word }}
        <span>({{ site.tags[this_word].size }})</span>
      </a> , 
  {% endunless %}{% endfor %}
</ul>


<!-- -----------------------Listado del Posts por Tag-------------------------------------------------------- -->
<div>

<a name="seccion3">Listado de Posts por etiquetas</a>  

<a href="#top">Volver al inicio</a>

{% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tag_words[item] }}{% endcapture %}
    <h2 id="{{ this_word | cgi_escape }}">{{ this_word }}</h2>
    {% for post in site.tags[this_word] %}{% if post.title != null %}
      <div>
        <span style="float: left;">
          <a href="{{ post.url }}">{{ post.title }}</a>
        </span>
        <span style="float: right;">
          {{ post.date | date_to_string }}
        </span>
      </div>
      <div style="clear: both;"></div>
    {% endif %}{% endfor %}
  {% endunless %}{% endfor %}
</div>
---
# Escucha los Podcast en ivoox
<a name="seccion1">ivoox</a>
<a href="#top">Volver al inicio</a>

<iframe src="https://www.ivoox.com/player_es_podcast_383493_1.html" width="100%" style="border: 1px solid #D7D7D7;" height="440" frameborder="0" allowfullscreen="0" scrolling="no" ></iframe> 

# Redes Sociales
<a name="seccion2">Twitter</a>
<a href="#top">Volver al inicio</a>
<a class="twitter-timeline" href="https://twitter.com/uGeekPodcast">Tweets by uGeekPodcast</a> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

<a href="#top">Volver al inicio</a>

 
