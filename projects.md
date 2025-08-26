---
layout: default
title: Projects
---
<main class="main-content">
<h1 class="projects-heading">{{ page.title }}</h1>

<div class="projects-list">
  {% for project in site.projects %}
    <a href="{{ project.url }}" class="project-row">
      <div class="project-content">
        <h2 class="project-title">{{ project.title }}</h2>
        <p class="project-dates">
        {{ project.start_date | date: "%B %Y" }} –
        {% if project.end_date %}
          {{ project.end_date | date: "%B %Y" }}
        {% else %}
          Present
        {% endif %}
      </p>
        <p class="project-description">{{ project.description }}</p>
      </div>
      {% if project.image %}
      <div class="project-image">
          <img src="{{ project.image }}" alt="{{ project.title }}">
      {% endif %}
      </div>
    </a>
  {% endfor %}
</div>
</main>

