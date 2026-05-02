<script>
	import { onMount } from 'svelte';
	import Navbar from '$lib/components/Navbar.svelte';
	import Footer from '$lib/components/Footer.svelte'
	import './layout.css';

	let { children } = $props();
//reveal and unreveal med scroll
	onMount(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('visible');
          } else {
            entry.target.classList.remove('visible');
          }
        });
      },
      { threshold: 0.15 }
    );

    document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
  });
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
