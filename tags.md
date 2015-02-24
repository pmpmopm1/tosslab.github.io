---
layout: default
category: tags
permalink: /tags/
title: JANDI tech blog
description: 안녕하세요. 잔디 서비스를 개발중인 토스랩 식구들의 블로그입니다.
---

{% for tag in site.iterable.tags %}
<h3>{{ tag.name }}</h3>
<ul>
    {% for post in tag.posts %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
        <time>{{ post.date | date: "%e %B %Y" }}</time>
    {% endfor %}
</ul>
{% endfor %}


<article>

{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
{% assign tag_words = site_tags | split:',' | sort %}
<div class="col-sm-3 col-xs-6">
    <ul class="nav nav-tabs-vertical">
    {% for item in (0..site.tags.size) %}{% unless forloop.last %}
      {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
      <li>
          <a href="#{{ this_word | replace:' ','-' }}-ref" data-toggle="tab">
            {{ this_word }}<span class="badge pull-right">{{ site.tags[this_word].size }}</span>
         </a>
      </li>
   {% endunless %}{% endfor %}
   </ul>
</div>
<!-- Tab panes -->
<div class="tab-content col-sm-9 col-xs-6">
  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
    <div class="tab-pane" id="{{ this_word | replace:' ','-' }}-ref">
      <h2 style="margin-top: 0px">Posts tagged  with {{ this_word }}</h2>
      <ul class="list-unstyled">
        {% for post in site.tags[this_word] %}{% if post.title != null %}
          <li style="line-height: 35px;"><a href="{{ site.BASE_PATH }}{{post.url}}">{{post.title}}</a> <span class="text-muted">- {{ post.date | date: "%B %d, %Y" }}</span></li>
        {% endif %}{% endfor %}
      </ul>
    </div>
  {% endunless %}{% endfor %}
</div>

</article>