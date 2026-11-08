---
layout: archive
title: ""
permalink: /nature/
author_profile: true
---

{% assign nature_images = site.static_files | where_exp: "file", "file.path contains '/images/nature/'" %}

{% if nature_images.size > 0 %}

![Nature photograph]({{ nature_images[0].path | relative_url }})

{% else %}

No nature photographs found.

{% endif %}
