---
layout: default
title: birdlog
permalink: /birdlog/
---

<!-- 1. Collect all bird entries across all posts into a single array -->
{% assign all_birds = "" | split: "" %}
{% for post in site.posts %}
  {% if post.birds %}
    {% assign all_birds = all_birds | concat: post.birds %}
  {% endif %}
{% endfor %}

<!-- 2. Remove duplicate bird species to get the distinct list and total count -->
{% assign distinct_birds = all_birds | uniq %}
{% assign bird_count = distinct_birds.size %}

<!-- Top Row: Title on left, Badge on right -->
<div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
  <h1 style="margin: 0;">birdlog</h1>
  
  <!-- Automatic Badge Counter -->
  <div style="background: #f8f9fa; border: 1px solid #e1e4e8; padding: 10px 14px; border-radius: 8px; font-size: 0.85rem; line-height: 1.5; white-space: nowrap; box-shadow: 0 1px 3px rgba(0,0,0,0.05);">
    <div>🐦‍⬛ Species blogged: <strong>{{ bird_count }}</strong></div>
    <div>🦉 Total species seen: <a href="https://ebird.org/profile/NjA3NDU4Nw" target="_blank" rel="noopener noreferrer" style="font-weight: bold; color: #2e7d32; text-decoration: none;">147 ↗</a></div>
  </div>
</div>

<!-- Intro Text (Sits underneath the title/badge row) -->
<p style="margin: 0 0 25px 0; color: #555;">This is the birdlog, or <em>blog</em>, for short (yes I definitely came up with that hip new word). Unless stated otherwise, any image or sound posted here is by me and is licensed under CC-BY-SA 4.0 ©birdlog.</p>

{% assign total_posts = site.posts | size %}

<ul style="list-style: none; padding-left: 0;">
  {% for post in site.posts %}
    {% assign post_num = total_posts | minus: forloop.index0 %}
    <li style="margin-bottom: 25px; display: flex; align-items: baseline;">
      
      <!-- Custom calculated post number -->
      <span style="font-weight: bold; margin-right: 12px; min-width: 25px; color: #444;">
        {{ post_num }}.
      </span>
      
      <!-- Post Title and Date -->
      <div>
        <a href="{{ post.url | relative_url }}" style="font-size: 1.1rem; font-weight: bold; text-decoration: none;">
          {{ post.title }}
        </a>
        <p style="margin: 4px 0 0 0; font-size: 0.85rem; color: #666;">
          {{ post.date | date: "%B %d, %Y" }}
        </p>
      </div>
      
    </li>
  {% endfor %}
</ul>
