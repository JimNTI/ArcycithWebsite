<script>
	import Navbar from '$lib/components/Navbar.svelte';
	import Footer from '$lib/components/Footer.svelte'
	import './layout.css';

	let { children } = $props();
</script>

<div class="site">

	<Navbar />

	<main>
		{@render children()}
	</main>

	<Footer />
</div>

<style>

.site{
	background: linear-gradient(135deg, #0f0f12 0%, #330066 100%);
}
</style>
