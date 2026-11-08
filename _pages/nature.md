
---
layout: archive
title: ""
permalink: /nature/
author_profile: true
redirect_from:
  - /nature
  - /nature.html
---

{% assign nature_images = site.static_files | where_exp: "file", "file.path contains '/images/nature/'" %}

{% if nature_images.size > 0 %}

<div class="nature-random-image">
  <img
    id="nature-image"
    src="{{ nature_images[0].path | relative_url }}"
    alt="Nature photography"
    style="display: block; width: 100%; max-width: 100%; height: auto;"
  >
</div>

<script>
(function() {
  const natureImages = [
    {% for image in nature_images %}
      {{ image.path | relative_url | jsonify }}{% unless forloop.last %},{% endunless %}
    {% endfor %}
  ];

  const randomIndex = Math.floor(Math.random() * natureImages.length);

  document.getElementById("nature-image").src =
    natureImages[randomIndex];
})();
</script>

{% else %}

<p>No nature photographs found.</p>

{% endif %}
