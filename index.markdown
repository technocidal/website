---
title: Home
---
<section>
	<article>
		<div class="grid">
			<img style="max-height: 15rem;" class="profile-picture" src="/assets/images/profile.png">
			<hgroup>
				<h2>My name is {{ site.author.name }}</h2>
				<p>I'm a father, software engineer and aspiring coffee snob.</p>
			</hgroup>
		</div>
	</article>
</section>

<section>
	<h2>Latest post</h2>
	{% for post in site.posts limit:1 %}
	<article>
		<hgroup>
		<h2>{{ post.title }}</h2>
		{{ post.excerpt }}
		</hgroup>
		<a style="text-decoration: none;" href="{{ post.url }}">Read more…</a>
	</article>
	{% endfor %}
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