---
layout: page
title: Projects
permalink: /projects/
description: Six core computational chemistry projects across machine learning, molecular modeling, and cheminformatics.
nav: true
nav_order: 3
display_categories: [Machine Learning, Molecular Modeling, Cheminformatics]
horizontal: false
---

These projects highlight my core workflows. Machine learning: discovering functional peptides with protein language models and MD, and late-fusion ML ensembles for hERG/CYP3K binder identification. Molecular modeling: structure-function relationships in EGFR, KRAS, and p53; ice growth inhibition by antifreeze peptides; a docking/MD/QM-MM workflow to prioritize EGFR inhibitors; and alchemical free-energy calculations for KRAS nucleotide binding. Cheminformatics: EnerGeom, energy/geometric descriptors for bioactive ligands.

<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}
{% assign sorted_projects = site.projects | sort: "importance" %}
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>
