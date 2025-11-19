---
layout: default
title: Categories
---
<div class="container mt-4">
  <h1 class="mb-4">Categories</h1>

  <div class="row" id="categories-container">
    {% assign all_categories = site.posts | map: "categories" | flatten | uniq %}
    {% for cat in all_categories %}
      <div class="col-md-4 py-2">
        <a href="{{ site.baseurl }}/categories/{{ cat | slugify }}/" class="text-decoration-none">
          <div class="card-custom text-center p-5 category-card" style="position: relative; border-radius: 10px; overflow: hidden;height: 121px;">
            <h3 class="category-title" style="position: relative; z-index: 2; color: white;">{{ cat }}</h3>
            <img src="https://picsum.photos/400/250?random={{ forloop.index }}" alt="{{ cat }}" style="position: absolute; top:0; left:0; width:100%; height:100%; object-fit: cover; filter: brightness(0.5); z-index:1;">
          </div>
        </a>
      </div>
    {% endfor %}
  </div>
</div>

<style>
.category-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 15px rgba(0,0,0,0.3);
  transition: all 0.2s;
}
.category-title {
  font-weight: bold;
}
</style>
