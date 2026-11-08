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

  if (natureImages.length === 0) return;

  let recentImages = [];

  try {
    recentImages = JSON.parse(
      sessionStorage.getItem(storageKey) || "[]"
    );
  } catch (error) {
    recentImages = [];
  }

  // Keep only images that still exist
  recentImages = recentImages.filter(
    image => natureImages.includes(image)
  );

  // Exclude the last two displayed photographs
  let availableImages = natureImages.filter(
    image => !recentImages.includes(image)
  );

  // If fewer than three photographs exist, reset the history
  if (availableImages.length === 0) {
    recentImages = [];
    availableImages = natureImages;
  }

  const selectedImage = availableImages[
    Math.floor(Math.random() * availableImages.length)
  ];

  recentImages.push(selectedImage);
  recentImages = recentImages.slice(-2);

  try {
    sessionStorage.setItem(
      storageKey,
      JSON.stringify(recentImages)
    );
  } catch (error) {
    // Continue displaying images if browser storage is unavailable
  }

  document.getElementById("nature-image").src = selectedImage;
})();
</script>

{% else %}

<p>No nature photographs found.</p>

{% endif %}
