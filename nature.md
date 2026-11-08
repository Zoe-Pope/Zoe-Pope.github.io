---
layout: archive
title: ""
permalink: /nature/
author_profile: true
---

{% assign nature_images = site.static_files | where_exp: "file", "file.path contains '/images/nature/'" %}

{% if nature_images.size > 0 %}

<div class="nature-random-image">
  <img
    id="nature-image"
    src="{{ nature_images[0].path | relative_url }}"
    alt="Nature photography"
    style="display: block; width: 100%; max-width: none; height: auto;"
  >
</div>

<script>
(function() {
  const natureImages = [
    {% for image in nature_images %}
      {{ image.path | relative_url | jsonify }}{% unless forloop.last %},{% endunless %}
    {% endfor %}
  ];

  const storageKey = "recentNatureImages";

  let recentImages = JSON.parse(
    sessionStorage.getItem(storageKey) || "[]"
  );

  // Exclude the last two photographs
  let availableImages = natureImages.filter(
    image => !recentImages.includes(image)
  );

  // If there are too few images, allow repeats rather than showing nothing
  if (availableImages.length === 0) {
    availableImages = natureImages;
  }

  const randomIndex = Math.floor(
    Math.random() * availableImages.length
  );

  const selectedImage = availableImages[randomIndex];

  // Remember the two most recently displayed photographs
  recentImages.push(selectedImage);
  recentImages = recentImages.slice(-2);

  sessionStorage.setItem(
    storageKey,
    JSON.stringify(recentImages)
  );

  document.getElementById("nature-image").src = selectedImage;
})();
</script>

{% else %}

<p>No nature photographs found.</p>

{% endif %}
