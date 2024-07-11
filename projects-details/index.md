---
layout: default
title: My Projects
---

# My Projects

{% for project in site.data.projects %}
## {{ projects.title }}

{{ projects.description }}

- {% for detail in projects.details %}{{ detail }}{% if forloop.last == false %},{% endif %}{% endfor %}

Link to Project
{% endfor %}
