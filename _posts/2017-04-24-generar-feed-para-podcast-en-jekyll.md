---
layout: page
title: "Crear el Feed para el podcast en tu Blog con Jekyll"
date: 2017-04-24
tags: [jekyll, blog, feed, podcast]
---
# Publicado por Angel

Voy a explicar en este post, como generar el Feed del podcast de forma automática.

* Creamos un archivo `podcast.xml` en la raiz, con el siguiente contenido:


{% highlight ruby %}

---
layout: null
---
<?xml version="1.0" encoding="UTF-8"?><rss version="2.0"
xmlns:content="http://purl.org/rss/1.0/modules/content/"
xmlns:wfw="http://wellformedweb.org/CommentAPI/"
xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:atom="http://www.w3.org/2005/Atom"
xmlns:sy="http://purl.org/rss/1.0/modules/syndication/"
xmlns:slash="http://purl.org/rss/1.0/modules/slash/"
xmlns:itunes="http://www.itunes.com/dtds/podcast-1.0.dtd"
xmlns:rawvoice="http://www.rawvoice.com/rawvoiceRssModule/"
>
 
<channel>
<title>{{ site.podcast_title }}</title>
<atom:link href="{{ site.url }}/feed/podcast" rel="self" type="application/rss+xml" />
<link>{{ site.url }}</link>
<description>{{ site.podcast_description }}</description>
<lastBuildDate>{{ site.time | date: "%a, %d %b %Y %H:%M:%S %z" }}</lastBuildDate>
<language>es-es</language>
<sy:updatePeriod>hourly</sy:updatePeriod>
<sy:updateFrequency>1</sy:updateFrequency>
<generator>http://jekyllrb.com</generator>
<itunes:summary>{{ site.podcast_summary }}</itunes:summary>
<itunes:author>{{ site.podcast_author }}</itunes:author>
<itunes:explicit>{{ site.podcast_explicit }}</itunes:explicit>
<itunes:image href="{{ site.url }}{{ site.podcast_album_art }}" />
<itunes:owner>
<itunes:name>{{ site.podcast_owner }}</itunes:name>
<itunes:email>{{ site.podcast_email }}</itunes:email>
</itunes:owner>
<managingEditor>{{ site.podcast_email }} ({{ site.podcast_owner }})</managingEditor>
<itunes:subtitle>{{ site.podcast_subtitle }}</itunes:subtitle>
<image>
<title>{{ site.podcast_title }}</title>
<url>{{ site.url }}{{ site.podcast_album_art }}</url>
<link>{{ site.url }}</link>
</image>
<itunes:category text="{{ site.podcast_category }}">
<itunes:category text="{{ site.podcast_subcategory_one }}" />
<itunes:category text="{{ site.podcast_subcategory_two }}" />
</itunes:category>
{% for ep in site.categories.podcast %}
  <item>
    <title>{{ ep.title }}</title>
    <link>{{ site.url }}{{ ep.url }}</link>
    <comments>{{ site.url }}{{ ep.url }}#comments</comments>
    <pubDate>{{ ep.date | date: "%a, %d %b %Y %T %z" }}</pubDate>
    <dc:creator><![CDATA[{{ site.author | cdata_escape }}]]></dc:creator>
{% for category in ep.categories %}
    <category><![CDATA[{{ category | cdata_escape }}]]></category>
{% endfor %}
{% for category in ep.tags %}
    <category><![CDATA[{{ category | cdata_escape }}]]></category>
{% endfor %}
    <guid isPermaLink="{% if ep.podcast_guid %}false{% else %}true{% endif %}">{{ site.url }}{% if ep.podcast_guid %}/{{ ep.podcast_guid }}{% else %}{{ ep.url }}{% endif %}</guid>
    <description>
        <![CDATA[{{ ep.excerpt | strip_html | truncatewords: 50 | expand_urls: site.url | cdata_escape }}]]>
    </description>
    <content:encoded>
        <![CDATA[{{ ep.content | expand_urls: site.url | cdata_escape }}]]>
    </content:encoded>

    <enclosure url="{{ ep.podcast_link }}" length="{{ ep.podcast_length }}" type="audio/mpeg" />
    <itunes:subtitle><![CDATA[{{ ep.excerpt | strip_html | truncatewords: 50 | expand_urls: site.url | cdata_escape }}]]></itunes:subtitle>
    <itunes:summary><![CDATA[{{ ep.content | expand_urls: site.url | cdata_escape }}]]></itunes:summary>
    <itunes:author>{{ site.podcast_author }}</itunes:author>
    <itunes:image href="{{ site.url }}{{ site.podcast_album_art }}" />
    <itunes:explicit>{{ site.podcast_explicit }}</itunes:explicit>
    <itunes:duration>{{ ep.podcast_duration }}</itunes:duration>
  </item>
{% endfor %}
</channel>
</rss>

{% endhighlight %}



* Añadimos en el archivo `_config.yml`, el siguiente contenido:

{% highlight ruby %}

# Podcast Feed Settings
podcast_url: https://ugeek.github.io
podcast_album_art: https://ugeek.github.io/img/ugeek.png
podcast_title: uGeek
podcast_owner: Angel
podcast_email: ugeekpodcast@gmail.com
podcast_category: Technology
podcast_subcategory_one: Linux
podcast_subcategory_two: Gadgets
podcast_explicit: "no"
podcast_author: Angel
podcast_description: Podcast de Tecnología en el que hablo de GNU/Linux, Raspberry Pi, servidores y tecnología en general.
podcast_summary: Podcast de Tecnología en el que hablo de GNU/Linux, Raspberry Pi, servidores y tecnología en general.
podcast_subtitle: Podcast de Tecnología en el que hablo de GNU/Linux, Raspberry Pi, servidores y tecnología en general.

{% endhighlight %}


* Por último, añadiremos en cada post, que es un podcast, el link del mp3, imagen, tags, etc...

{% highlight ruby %}

---
layout: post
title: "046. Sincronización de carpetas entre dispositivos. Syncthing, Resilio y Dukto"
date: 2017-04-21
categories: podcast
image: img/ugeek.png
podcast_link: https://ia601509.us.archive.org/6/items/046SyncthingResilioYDukto/%23046%20Syncthing%2c%20Resilio%20y%20Dukto%20.mp3
tags: [syncthing, resilio, dukto, sincronización carpetas, podcast]
comments: true
---

{% endhighlight %}

