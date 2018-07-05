---
layout: page
title: Editions
permalink: /editions/
exclude_from_menu: true

---

# Current Edition

**{{ site.data.editions[0].frontmatter }}**: {{ site.data.editions[0].changes }}.

[Go to edition {{site.data.editions[0].edition}}](/notes/)

# Editions

{% for edition in site.data.editions %}
* {{ edition.edition }} 

    **{{edition.frontmatter}}**: {{ edition.changes }}
      
{% endfor %}

