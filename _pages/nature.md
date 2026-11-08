
---
layout: archive
title: ""
permalink: /nature/
author_profile: true
redirect_from:
  - /nature
  - /nature.html
---

{% raw %}{% assign nature_images = site.static_files | where_exp: "file", "file.path contains '/images/nature/'" %}

{% if nature_images.size > 0 %}
<script>
const natureImages = [
  {% for image in nature_images %}
    {{ image.path | relative_url | jsonify }}{% unless forloop.last %},{% endunless %}
  {% endfor %}
];

const randomIndex = Math.floor(Math.random() * natureImages.length);

document.write(
  '<img src="' + natureImages[randomIndex] +
  '" alt="Nature photography" ' +
  'style="display:block;width:100%;height:auto;">'
);
</script>
{% else %}
<p>No nature photographs found.</p>
{% endif %}{% endraw %}
