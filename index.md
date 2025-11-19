---
layout: default
---

<div class="container mt-4">
  <!-- Arama Kutusu -->
  <div class="search-article mb-4">
    <label for="search-input" class="search-icon">
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" stroke="rgba(128,128,128,0.8)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <circle cx="11" cy="11" r="8"></circle>
        <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
      </svg>
    </label>
    <input type="search" id="search-input" placeholder="Find some link here" aria-label="Search">
  </div>

  <!-- Blog Kartları -->
  <div class="row" id="posts-container">
    {% for post in site.posts %}
      <div class="col-md-4 py-2 post-card">
      <div class="card-custom">
      <!-- BAYRAK BURAYA GELECEK -->
      <span  class="flag-badge">
        {% if post.lang %}
        <img src="https://flagcdn.com/48x36/{{ post.lang }}.png" alt="{{ post.lang }}">
        {% else %}
    🌍
        {% endif %}
      </span >
        <a href="{{ site.baseurl }}{{ post.url }}" class="text-decoration-none">
          <div class="card-custom">
            <!--<img src="https://picsum.photos/400/250?4" alt="Site 1">-->
            <img src="{{ post.image | default: '/assets/img/default-post-bg.webp' }}" alt="{{ post.title }}">
            <div class="card-overlay">
              <h5>{{ post.title }}</h5>
              <p>{{ post.desc }}</p>
              <p><small class="text-white">{{ post.date | date: "%d %B %Y" }}</small></p>
            </div>
          </div>
        </a>
        </div> 
      </div>  
    {% endfor %}
  </div>
</div>

<!-- Arama Scripti -->
<script>
const searchInput = document.getElementById('search-input');
const posts = document.querySelectorAll('.post-card');

searchInput.addEventListener('input', () => {
  const query = searchInput.value.toLowerCase().trim();
  let foundAny = false;

  posts.forEach(post => {
    const title = post.querySelector('h5').textContent.toLowerCase();
    const desc = post.querySelector('p').textContent.toLowerCase();

    if (title.includes(query) || desc.includes(query)) {
      post.style.display = 'block';
      foundAny = true;
    } else {
      post.style.display = 'none';
    }
  });

  // Sonuç yoksa mesaj göster
  let noResults = document.getElementById('no-results');
  if (!foundAny) {
    if (!noResults) {
      noResults = document.createElement('p');
      noResults.id = 'no-results';
      noResults.textContent = '404 - We searched and did not find!';
      noResults.style.color = 'red';
      noResults.style.textAlign="center";
      searchInput.parentNode.after(noResults);
    }
  } else if (noResults) {
    noResults.remove();
  }
});
</script>
