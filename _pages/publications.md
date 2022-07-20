---
layout: page
permalink: /publications/
title: publications
description: See updated list on <a href='https://scholar.google.com/citations?user=FvPXxs0AAAAJ&hl=en'> Google Scholar </a>.
years: [current, 2022, 2021, 2020, 2019, 2018, 2017, 2016, 2015]
categories: ['Working Papers', 'Work-in-progress', 'Published Papers']
catprint: ['', 'Working Papers', 'Work-in-progress', 'Published Papers', 'Conferences', 'Posters']
nav: true
nav_order: 1
---
<!-- _pages/publications.md -->
<div class="publications">

{% for cat_ in page.categories  %}
	{% assign ind = forloop.index %}

	{%- capture cat -%}
 		{% if page.catprint[ind] == "Work-in-progress" -%}
			Work-in-progress <h6 class="mb-n4 mt-3 pt-2 mp-5">Correct authoring will be determined later</h6>
		{% elsif page.catprint[ind] == "Published Papers" -%}
			Selected {{ page.catprint[ind] }}
		{%- else %}
			{{ page.catprint[ind] }}
		{% endif %}
	{%- endcapture -%}
	
	<h4 class="font-weight-bolder mb-n4 mt-5 mp-5">{{cat}}</h4>
	{% for y in page.years  %}
		{%- capture citecount -%}
		{% bibliography_count -f papers -q @*[kind={{cat_}} && year={{y}}]* %}
		{%- endcapture -%}

		{% if citecount != "0"  %}
			<h2 class="year">{{y}}</h2>
			{% bibliography -f papers -q @*[kind={{cat_}} && year={{y}}]* %}
		{% endif %}
	{% endfor %}
{% endfor %}

</div>
