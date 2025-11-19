---
layout: default
title: Education
category: Education
permalink: /categories/education/
---
<div class="container mt-4">
  <h1>Category: {{ page.category }}</h1>

  <div class="row" id="posts-container">
    {% for post in site.posts %}
      {% if post.categories contains page.category %}
        <div class="col-md-4 py-2 post-card">
          <div class="card-custom">
            <span class="flag-badge">
              {% if post.lang %}
                <img src="https://flagcdn.com/48x36/{{ post.lang }}.png" alt="{{ post.lang }}">
              {% else %}
                🌍
              {% endif %}
            </span>
            <a href="{{ site.baseurl }}{{ post.url }}" class="text-decoration-none">
              <div class="card-custom">
                <img src="{{ post.image | default: site.favicon }}" alt="{{ post.title }}">
                <div class="card-overlay">
                  <h5>{{ post.title }}</h5>
                  <p>{{ post.desc }}</p>
                  <p><small class="text-white">{{ post.date | date: "%d %B %Y" }}</small></p>
                </div>
              </div>
            </a>
          </div>
        </div>
      {% endif %}
    {% endfor %}
  </div>
</div>
