--- 
layout: default 
title: Projects
permalink: /projects/ 
---
<div id="archive">
  {% for project in site.projects %}
    <div class="archive__block">
      <h2 class="archive__year"><a href="{{ project.url | prepend: site.baseurl }}">{{ project.title }}</a></h2>
      <p>{{ project.description }}</p>
    </div>
  {% endfor %}
</div>