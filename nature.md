---
layout: archive
title: ""
permalink: /nature/
author_profile: true
---

{% assign nature_images = site.static_files | where_exp: "file", "file.path contains '/images/nature/'" %}
{% assign nature_paths = nature_images | map: "path" %}

<div class="nature-random-image">
  <img
    id="nature-image"
    alt="Random nature photograph"
    style="display: none; width: 100%; max-width: none; height: auto;"
  >
</div>

<script>
(function() {

  // All photographs discovered by Jekyll
  const natureImages = {{ nature_paths | jsonify }};

  // Remember the last two photographs
  const storageKey = "recentNatureImages";

  const imageElement = document.getElementById("nature-image");

  if (!natureImages || natureImages.length === 0) {
    console.error("No nature photographs found.");
    return;
  }

  let recentImages = [];

  try {
    recentImages = JSON.parse(
      sessionStorage.getItem(storageKey) || "[]"
    );
  } catch (error) {
    recentImages = [];
  }

  // Only retain photographs that still exist
  recentImages = recentImages.filter(
    image => natureImages.includes(image)
  ).slice(-2);

  // Exclude the last two photographs
  const availableImages = natureImages.filter(
    image => !recentImages.includes(image)
  );

  // Randomly select from the remaining photographs
  const selectedImage = availableImages[
    Math.floor(Math.random() * availableImages.length)
  ];

  // Display the selected photograph
  imageElement.src = selectedImage;
  imageElement.style.display = "block";

  // Update the viewing history
  recentImages.push(selectedImage);

  try {
    sessionStorage.setItem(
      storageKey,
      JSON.stringify(recentImages.slice(-2))
    );
  } catch (error) {
    console.warn("Could not save image history.");
  }

})();
</script>

<p style="text-align:center; font-size:0.8em; color:gray;">
  {{ nature_images.size }} photographs in collection
</p>
