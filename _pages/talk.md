---
layout: page
permalink: /talks/
title: talks
description: talks in industrial conference
years: [2023, 2022, 2020]
nav: true
nav_order: 1
---
<!-- _pages/publications.md -->
<div class="talk">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% talk -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>
