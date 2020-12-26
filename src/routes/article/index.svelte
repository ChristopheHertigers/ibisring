<script context="module">
	export function preload() {
		return this.fetch(`article.json`).then(r => r.json()).then(posts => {
			return { posts };
		});
	}
</script>

<script>
	export let posts;
</script>

<style>
	ul {
		margin: 0 0 1em 0;
		line-height: 1.5;
	}

	a.hidden {
	    display: none;
	}
</style>

<svelte:head>
	<title>Articles</title>
</svelte:head>

<h1>Recent posts</h1>

<ul>
	{#each posts as post}
		<!-- we're using the non-standard `rel=prefetch` attribute to
				tell Sapper to load the data for the page as soon as
				the user hovers over the link or taps it, instead of
				waiting for the 'click' event -->
		<li><a rel="prefetch" href="article/{post.slug}">{post.title}</a> <a class="hidden" href="article/{post.slug}.json">json</a></li>
	{/each}
</ul>
