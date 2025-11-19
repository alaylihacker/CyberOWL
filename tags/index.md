---
layout: default
title: Tags
---

<div class="container mt-4">

  <h1 class="mb-4">Tags</h1>

  <div id="tag-cloud" class="mb-4"></div>

  <hr>

  <div id="tag-results" style="display:none;">
    <h2 id="selected-tag-title" class="mb-3"></h2>
    <ul id="tag-post-list"></ul>
  </div>

</div>

<style>
.tag-item {
  margin: 5px 10px;
  display: inline-block;
  cursor: pointer;
  font-weight: 600;
  color: #0d6efd;
}

.tag-item:hover {
  text-decoration: underline;
}
</style>

<script>
  // Postları alıyoruz
  const posts = [
    {% for post in site.posts %}
      {
        "title": "{{ post.title | escape }}",
        "url": "{{ site.baseurl }}{{ post.url }}",
        "tags": [{% for t in post.tags %}"{{ t }}"{% if forloop.last == false %}, {% endif %}{% endfor %}]
      }{% if forloop.last == false %}, {% endif %}
    {% endfor %}
  ];

  // Tag sayıları
  const tagCounts = {};

  posts.forEach(post => {
    post.tags.forEach(t => {
      tagCounts[t] = (tagCounts[t] || 0) + 1;
    });
  });

  // Font size hesaplama
  const minFont = 14;
  const maxFont = 32;
  const maxCount = Math.max(...Object.values(tagCounts));

  const tagCloudDiv = document.getElementById("tag-cloud");

  Object.keys(tagCounts).forEach(tag => {
    const count = tagCounts[tag];
    const size = minFont + (count / maxCount) * (maxFont - minFont);

    const span = document.createElement("span");
    span.className = "tag-item";
    span.style.fontSize = size + "px";
    span.dataset.tag = tag;
    span.innerText = `${tag} (${count})`;

    tagCloudDiv.appendChild(span);

    span.addEventListener("click", () => {
      const filtered = posts.filter(p => p.tags.includes(tag));

      document.getElementById("selected-tag-title").innerText = "Tag posts: " + tag;

      document.getElementById("tag-post-list").innerHTML =
        filtered.map(p => `<li><a href="${p.url}">${p.title}</a></li>`).join("");

      document.getElementById("tag-results").style.display = "block";

      window.scrollTo({ top: document.getElementById("tag-results").offsetTop - 50, behavior: "smooth" });
    });
  });
</script>
