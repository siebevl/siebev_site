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

<div style="margin-bottom: 25px;">
  <a href="{{ '/feed.xml' | relative_url }}" class="rss-link" title="Subscribe via RSS">
    <svg class="rss-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
      <circle cx="6.18" cy="17.82" r="2.18"/>
      <path d="M4 4.44v2.83c7.03 0 12.73 5.7 12.73 12.73h2.83c0-8.59-6.97-15.56-15.56-15.56z"/>
      <path d="M4 10.1v2.83c3.9 0 7.07 3.17 7.07 7.07h2.83c0-5.47-4.43-9.9-9.9-9.9z"/>
    </svg>
    <span>Subscribe via RSS</span>
  </a>
</div>

<style>
  .rss-link {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    text-decoration: none;
    color: #444;
    font-weight: 500;
  }

  .rss-icon {
    width: 20px;
    height: 20px;
    color: #ee802f;
    transition: transform 0.2s ease, opacity 0.2s ease;
  }

  .rss-link:hover .rss-icon {
    transform: scale(1.1);
    opacity: 0.85;
  }

  .rss-link:hover span {
    text-decoration: underline;
  }
</style>
