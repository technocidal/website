---
title: Home
---
<article>
	<div class="grid">
		<img style="max-height: 15rem;" class="profile" src="/assets/images/profile.png">
		<hgroup>
			<h2>My name is {{ site.author.name }}</h2>
			<p>I'm a father, software engineer and aspiring coffee snob.</p>
		</hgroup>
	</div>
</article>

## Latest post

{% for post in site.posts limit:1 %}
<article>
	<hgroup>
	<h2><a style="text-decoration: none;" href="{{ post.url }}">{{ post.title }}</a></h2>
	{{ post.excerpt }}
	</hgroup>
	<a style="text-decoration: none;" href="{{ post.url }}">Read more…</a>
</article>
{% endfor %}

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