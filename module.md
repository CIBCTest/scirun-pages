---
title: SCIRun Module Documentation
category: info
tags: module
---

# SCIRun Modules

{% comment %}from https://gist.github.com/pepelsbey/9334494{% endcomment %}
{% capture tmp %}
{% for page in site.pages %}{% if page.category == "moduledocs" %} {{ page.module.category }} {% endif %}{% endfor %}
{% endcapture %}

{% assign categories = tmp | split: '  ' %}
{% assign tmp = categories[0] %}

{% for cat in categories %}
  {% unless tmp contains cat %}
    {% capture tmp  %} {{ tmp }} {{ cat }} {% endcapture %}
  {% endunless %}
{% endfor %}

{% assign modulecategories = tmp | split: ' ' %}

{% capture modulepages %}{% for cat in modulecategories %}?{{ cat }}{% for page in site.pages %}{% if page.module.category == cat %}${{ page.title }}#{{ site.github.url }}{{ page.url }}{% endif %}{% endfor %}{% endfor %}{% endcapture %}

{% assign sortedpages = modulepages | split: '?' | sort %}

{% for pagestring in sortedpages %}
  {% assign pageitems = pagestring | split: '$' %}
  {% if pageitems[0] %}
## {{ pageitems[0] | strip_newlines }}
    {% for item in pageitems %}
      {% if forloop.first %} {% continue %} {% endif %}
      {% assign linkitem = item | split: '#' %}
**[{{ linkitem[0] }}]({{ site.github.url }}{{ linkitem[1] }})**
    {% endfor %}
  {% endif %}
{% endfor %}
