---
title: Sitemap
desc: A full listing of published pages on the wiki.
layout: default
published: true
indexed: true
categories: [Wiki]
---
{% include header.html %}

{% for cat in site.category-list %}
### {{ cat }}
<ul>
{% for page in site.pages %}
{% if page.published == true %}
{% for pc in page.categories %}
{% if pc == cat %}
<li>
  <a href="/Ruby_for_Dragons{{ page.url }}">{{ page.title }}</a> &mdash; {{ page.desc }}
</li>
{% endif %} <!-- cat-match-p -->
{% endfor %} <!-- page-category -->
{% endif %} <!-- published-p -->
{% endfor %} <!-- page -->
</ul>
{% endfor %} <!-- cat -->
