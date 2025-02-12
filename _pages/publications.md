---
layout: page
permalink: /research/
title: Research
description: Please see more complete list of publications on <a href='https://scholar.google.com/citations?user=FvPXxs0AAAAJ&hl=en' style='color:#B509AC'> Google Scholar</a>.<br>The corresponding author is denoted by * . 
categories: ['Published Papers', 'Working Papers', 'Work-in-progress']
catprint: ['', 'Working Papers', 'Work-in-progress', 'Published Papers', 'Conferences', 'Posters']
nav: true
nav_order: 1
---

<!-- _pages/publications.md -->
<div class="publications">

  {% comment %} Set up dynamic years {% endcomment %}
  {% assign current_year = site.time | date: "%Y" | plus: 0 %}
  {% assign max_year = current_year | plus: 2 %}
  {% assign base_year = 2015 %}
  {% assign special_years = "current,forthcoming" | split: "," %}
  {% assign numeric_years = '' | split: '' %}
  {% for year in (base_year..max_year) reversed %}
    {% assign numeric_years = numeric_years | push: year %}
  {% endfor %}
  {% assign years = special_years | concat: numeric_years %}

  {% for cat_ in page.categories  %}
    {% assign ind = forloop.index %}
    {%- capture cat -%}
      {% if page.catprint[ind] == "Work-in-progress" -%}
        Work-in-progress <h6 class="mb-n4 mt-3 pt-2 mp-5">Correct authoring will be determined later</h6>
      {% elsif page.catprint[ind] == "Published Papers" -%}
        Selected {{ page.catprint[ind] }}
      {%- else -%}
        {{ page.catprint[ind] }}
      {% endif %}
    {%- endcapture -%}
    
    <h4 class="font-weight-bolder mb-n4 mt-5 mp-5">{{ cat }}</h4>
    {% for y in years %}
      {%- capture citecount -%}
        {% bibliography_count -f papers -q @*[kind={{ cat_ }} && year={{ y }}]* %}
      {%- endcapture -%}
  
      {% if citecount != "0" %}
        <h2 class="year">{{ y }}</h2>
        {% bibliography -f papers -q @*[kind={{ cat_ }} && year={{ y }}]* %}
      {% endif %}
    {% endfor %}
  {% endfor %}

</div>