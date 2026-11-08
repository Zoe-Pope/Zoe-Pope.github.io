---
layout: archive
title: ""
permalink: /nature/
author_profile: true
---

{% assign nature_images = site.static_files | where_exp: "file", "file.path contains '/images/nature/'" %}

<p>Images found: {{ nature_images.size }}</p>

<img
  src="{{ nature_images[0].path | relative_url }}"
  alt="Nature photograph"
  style="display:block; width:100%; height:auto;"
>
