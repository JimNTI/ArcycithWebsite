<script>
	import Header from '$lib/components/Header.svelte';
	import Hero from '$lib/components/Hero.svelte'
	import SocialMediaShowcase from '$lib/components/SocialMediaShowcase.svelte'
	import './layout.css';

	let { children } = $props();
</script>

<div class="site">

	<Header />

	<main>
		{@render children()}
	</main>

	<footer class="footer">
		<p>Arcycith</p>
	</footer>
</div>

<style>
	.site {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		margin: 0 auto;
		box-sizing: border-box;
		background-color: aliceblue;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 12px;
	}

	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
		}
	}
</style>
