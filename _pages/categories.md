---
layout: page
title: Categories
permalink: /categories/
---

{% assign sorted_categories = site.categories | sort %}

<h1>Categories</h1>

<ul>
  {% for category in sorted_categories %}
    {% assign category_name = category[0] %}
    {% assign posts = category[1] %}

    <li>
      <h2>{{ category_name }}</h2>
      <ul>
        {% for post in posts %}
          <li>
            <a href="{{ post.url }}">{{ post.title }}</a>
            <span> - {{ post.date | date: "%Y-%m-%d" }}</span>
          </li>
        {% endfor %}
      </ul>
    </li>
  {% endfor %}
</ul>
