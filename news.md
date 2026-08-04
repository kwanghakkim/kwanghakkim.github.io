---
layout: page
title: News
---

<!-- All items come from _data/news.yml (newest first, add at top).
     Entries are grouped by the trailing year of each item's date,
     preserving the manual file order — no date parsing involved. -->

{% assign current_year = "" %}
{% for item in site.data.news %}
{% assign item_year = item.date | split: " " | last %}
{% if item_year != current_year %}
{% unless forloop.first %}</ul>{% endunless %}
<h2 class="section-label news-year">{{ item_year }}</h2>
<ul class="news-list">
{% assign current_year = item_year %}
{% endif %}
<li>
  <span class="news-date">{{ item.date }}</span>
  <span class="news-text">{% if item.link %}<a href="{{ item.link }}">{{ item.text }}</a>{% else %}{{ item.text }}{% endif %}</span>
</li>
{% endfor %}
</ul>
