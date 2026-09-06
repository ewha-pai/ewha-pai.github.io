---
layout: page
title: Gallery
permalink: /gallery/
description: A look at life in the lab.
nav: true
nav_order: 3
---

<div class="gallery-filters">
  <button class="gallery-filter-btn active" data-category="all" type="button">All</button>
  {%- assign gallery_categories = "Lab Life,Research,Events,Retreats" | split: "," -%}
  {%- for category in gallery_categories -%}
  <button class="gallery-filter-btn" data-category="{{ category | slugify }}" type="button">{{ category }}</button>
  {%- endfor -%}
</div>

<div class="gallery-grid">
  {%- for item in site.data.gallery -%}
  <div class="gallery-item" data-category="{{ item.category | slugify }}">
    <img src="{{ item.image | relative_url }}" alt="{{ item.title }}" loading="lazy">
    <div class="gallery-overlay">
      <span class="gallery-title">{{ item.title }}</span>
      <span class="gallery-meta">{{ item.category }} &middot; {{ item.date | date: "%b %-d, %Y" }}</span>
    </div>
  </div>
  {%- endfor -%}
</div>

<style>
  .gallery-filters {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 0.5rem;
    margin: 0.5rem 0 2rem;
  }

  .gallery-filter-btn {
    padding: 0.4rem 1.1rem;
    border-radius: 999px;
    border: 1px solid var(--global-divider-color);
    background: var(--global-bg-color);
    color: var(--global-text-color);
    font-size: 0.9rem;
    cursor: pointer;
    transition: background-color 0.2s ease, color 0.2s ease, border-color 0.2s ease;
  }

  .gallery-filter-btn:hover {
    border-color: var(--global-theme-color);
  }

  .gallery-filter-btn.active {
    background: var(--global-theme-color);
    border-color: var(--global-theme-color);
    color: #fff;
  }

  .gallery-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1.25rem;
  }

  @media (max-width: 768px) {
    .gallery-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 480px) {
    .gallery-grid {
      grid-template-columns: 1fr;
    }
  }

  .gallery-item {
    position: relative;
    overflow: hidden;
    border-radius: 0.75rem;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.15);
    aspect-ratio: 4 / 3;
  }

  .gallery-item img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }

  .gallery-overlay {
    position: absolute;
    inset: 0;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding: 0.9rem;
    background: linear-gradient(to top, rgba(0, 0, 0, 0.75), rgba(0, 0, 0, 0) 65%);
    color: #fff;
    opacity: 0;
    transition: opacity 0.25s ease;
  }

  .gallery-item:hover .gallery-overlay {
    opacity: 1;
  }

  .gallery-title {
    color: #fff;
    font-weight: 600;
    font-size: 0.95rem;
    line-height: 1.3;
  }

  .gallery-meta {
    color: #fff;
    font-size: 0.8rem;
    opacity: 0.85;
    margin-top: 0.15rem;
  }
</style>

<script>
  document.addEventListener('DOMContentLoaded', function () {
    var buttons = document.querySelectorAll('.gallery-filter-btn');
    var items = document.querySelectorAll('.gallery-item');

    buttons.forEach(function (button) {
      button.addEventListener('click', function () {
        buttons.forEach(function (b) { b.classList.remove('active'); });
        button.classList.add('active');

        var category = button.getAttribute('data-category');
        items.forEach(function (item) {
          var show = category === 'all' || item.getAttribute('data-category') === category;
          item.style.display = show ? '' : 'none';
        });
      });
    });
  });
</script>
