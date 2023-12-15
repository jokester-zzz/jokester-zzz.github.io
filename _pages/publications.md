---
layout: page
permalink: /publications/
title: Publications
description: publications by categories in reversed chronological order. 
years: [2023, 2022, 2021, 2020]
ignore_years_published: [2019, 2018, 2017, 2016, 2015]
ignore_years_preprint: [2022, 2021, 2020, 2019, 2018, 2017, 2016, 2015]
nav: true
nav_order: 1
---

[[Published Papers](#published-papers)]
[[Preprints](#preprints)]

#### published papers

<div class="publications">

{% for y in page.years %}
  	{% unless page.ignore_years_conf contains y %}
      <h2 class="year">{{y}}</h2>
      {% bibliography -f published-papers -q @*[year={{y}}]* %}
    {% endunless %}
{% endfor %}

</div>


#### Preprints

<div class="publications">

{% for y in page.years %}
  	{% unless page.ignore_years_preprint contains y %}
      	<h2 class="year">{{y}}</h2>
      	{% bibliography -f preprints -q @*[year={{y}}]* %}
   	{% endunless %}
{% endfor %}

</div>
