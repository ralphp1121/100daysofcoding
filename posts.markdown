---
layout: page
title: Posts
permalink: /posts/
---

<div class="archive">
{% assign posts_by_year = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
{% if posts_by_year.size > 0 %}
  {% for year_group in posts_by_year %}
  <div class="archive-year">
    <h2 class="archive-year-title">{{ year_group.name }}</h2>
    {% assign posts_by_month = year_group.items | group_by_exp: "post", "post.date | date: '%B'" %}
    {% for month_group in posts_by_month %}
    <div class="archive-month">
      <h3 class="archive-month-title">{{ month_group.name }}</h3>
      <ul class="archive-post-list">
        {% for post in month_group.items %}
        <li class="archive-post-item">
          <a class="archive-post-link" href="{{ post.url | relative_url }}">
            <span class="archive-post-date">{{ post.date | date: "%b %-d" }}</span>
            <span class="archive-post-title">{{ post.title }}</span>
          </a>
        </li>
        {% endfor %}
      </ul>
    </div>
    {% endfor %}
  </div>
  {% endfor %}
{% else %}
  <p class="dashboard-empty">No posts yet — day 1 is coming soon.</p>
{% endif %}
</div>
