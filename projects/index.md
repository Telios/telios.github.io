---
layout: page
title: Projects
permalink: /projects/
---

{% assign all_projects = site.projects | sort: "order" %}
{% assign tag_list = "" | split: "" %}
{% for project in all_projects %}
  {% if project.tags %}
    {% for tag in project.tags %}
      {% unless tag_list contains tag %}
        {% assign tag_list = tag_list | push: tag %}
      {% endunless %}
    {% endfor %}
  {% endif %}
{% endfor %}

<div class="tag-row" data-tag-filters>
  <button class="tag-button is-active" type="button" data-tag="all">All</button>
  {% for tag in tag_list %}
    <button class="tag-button" type="button" data-tag="{{ tag | downcase }}">{{ tag }}</button>
  {% endfor %}
</div>

<div class="project-grid" data-project-grid>
  {% for project in all_projects %}
    {% assign tag_string = project.tags | join: ',' | downcase %}
    <article class="project-card" data-tags="{{ tag_string }}">
      <a href="{{ project.url | relative_url }}">
        <div class="project-media">
          {% if project.teaser_image %}
            <img src="{{ project.teaser_image | relative_url }}"
                 alt="{{ project.title }} teaser"
                 loading="lazy"
                 data-theme-img
                 data-light="{{ project.teaser_image | relative_url }}"
                 data-dark="{{ project.teaser_image_dark | default: project.teaser_image | relative_url }}" />
          {% else %}
            <div class="project-placeholder"></div>
          {% endif %}
        </div>
        <div class="project-body">
          <h3>{{ project.title }}</h3>
          <p>{{ project.description }}</p>
          {% if project.tags %}
            <div class="project-tags">
              {% for tag in project.tags %}
                <span>{{ tag }}</span>
              {% endfor %}
            </div>
          {% endif %}
          <span class="project-link">View project</span>
        </div>
      </a>
    </article>
  {% endfor %}
</div>

<script>
  (function () {
    var filters = document.querySelectorAll("[data-tag-filters] .tag-button");
    var cards = document.querySelectorAll("[data-project-grid] .project-card");
    if (!filters.length || !cards.length) return;
    filters.forEach(function (button) {
      button.addEventListener("click", function () {
        var tag = button.getAttribute("data-tag");
        filters.forEach(function (item) {
          item.classList.toggle("is-active", item === button);
        });
        cards.forEach(function (card) {
          var tags = card.getAttribute("data-tags") || "";
          var match = tag === "all" || tags.split(",").includes(tag);
          card.style.display = match ? "" : "none";
        });
      });
    });
  })();
</script>
