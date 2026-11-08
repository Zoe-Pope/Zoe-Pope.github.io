---
layout: archive
title: ""
permalink: /nature/
author_profile: true
---

{% assign nature_images = site.static_files | where_exp: "file", "file.path contains '/images/nature/'" %}

{% assign nature_paths = nature_images | map: "path" %}

<div id="nature-random-photo"></div>

<script>
(function() {
  const natureImages = {{ nature_paths | jsonify }};
  const storageKey = "recentNatureImages";

  if (!natureImages.length) return;

  let recentImages = [];

  try {
    recentImages = JSON.parse(
      sessionStorage.getItem(storageKey) || "[]"
    );
  } catch (error) {
    recentImages = [];
  }

  recentImages = recentImages
    .filter(image => natureImages.includes(image))
    .slice(-2);

  const availableImages = natureImages.filter(
    image => !recentImages.includes(image)
  );

  const selectedImage = availableImages[
    Math.floor(Math.random() * availableImages.length)
  ];

  recentImages.push(selectedImage);

  try {
    sessionStorage.setItem(
      storageKey,
      JSON.stringify(recentImages.slice(-2))
    );
  } catch (error) {}

  const image = document.createElement("img");
  image.src = selectedImage;
  image.alt = "Nature photography";
  image.style.width = "100%";
  image.style.maxWidth = "none";
  image.style.height = "auto";
  image.style.display = "block";

  document.getElementById("nature-random-photo").appendChild(image);
})();
</script>
