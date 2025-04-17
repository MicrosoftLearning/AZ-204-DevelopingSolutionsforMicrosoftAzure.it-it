---
title: Istruzioni ospitate online
permalink: index.html
layout: home
---

## Directory contenuto

In basso sono elencati i collegamenti ipertestuali a tutti i lab.

## Esercitazioni

{% assign labs = site.pages | where_exp: "page", "page.url contains '/Instructions/Labs'" %}
| Modulo | Lab |
| --- | --- |
{% per l'attività nei lab %} {% se activity.lab.az204Module %}| {{ activity.lab.az204Module }} | [{{ activity.lab.az204Title }}]({{ site.github.url }}{{ activity.url }}) |
{% endif %}{% endfor %}

