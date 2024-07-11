---
layout: default
title: My Projects
---

# My Projects

{% for project in site.data.projects %}
## {{ project.title }}

{{ project.description }}

- {% for detail in project.details %}{{ detail }}{% if forloop.last == false %},{% endif %}{% endfor %}

Link to Project
{% endfor %}
