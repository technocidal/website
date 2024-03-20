---
title: Home
---

<section style="padding-top: 0">
  <ul class="post-list">
    {% for post in site.posts %}
      <li class="post-list-element">
        {% include post-card.html post=post %}
      </li>
    {% endfor %}
  </ul>
</section>

<script>
  if (window.netlifyIdentity) {
	window.netlifyIdentity.on("init", user => {
	  if (!user) {
		window.netlifyIdentity.on("login", () => {
		  document.location.href = "/admin/";
		});
	  }
	});
  }
</script>