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

  <ul class="post-list">
    {% for post in site.posts %}
      <li class="post-list-element">
        <article>
          <hgroup>
          <h2>{{ post.title }}</h2>
          {{ post.excerpt }}
          </hgroup>
          <a href="{{ post.url }}">Read more…</a>
        </article>
      </li>
    {% endfor %}
  </ul>
</section>