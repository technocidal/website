---
title: Blog
---
<style>
  .post-list {
    margin-left: 0;
    padding-left: 0;
  }

  .post-list-element {
    list-style: none;
  }

  .post-list-element a {
    text-decoration: none;
  }
</style>

<section>
  <h1>Posts</h1>
</section>

<section>
  <ul class="post-list">
    {% for post in site.posts %}
      <li class="post-list-element">
        {% include post-card.html post=post %}
      </li>
    {% endfor %}
  </ul>
</section>