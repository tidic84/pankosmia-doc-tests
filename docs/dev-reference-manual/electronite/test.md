---
layout: default
title: Electron tips
permalink: /tests/
parent: Electronite
---

{{ site.data.lexique.mot1 }}
{{ site.data.lexique.mot2 }}

{% for entry in site.data.lexique %}
    console.log('{{ entry }}');
  {% endfor %}
