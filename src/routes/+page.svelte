<script>
	import Hero from '$lib/components/Hero.svelte';
	import SocialMediaShowcase from '$lib/components/SocialMediaShowcase.svelte';
	import AboutMe from '$lib/components/AboutMe.svelte';
	import GoalsLayout from '$lib/components/GoalsLayout.svelte';
	import ChallengesLayout from '$lib/components/ChallengesLayout.svelte';
</script>

<svelte:head>
	<title>Arcycith</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="min-h-screen bg-[#08080f]">
	<Hero />
	<div class="min-h-screen">
	<div class="reveal">
	<SocialMediaShowcase /></div>
	<div class=""><AboutMe /></div>
	<div class="reveal"><GoalsLayout /></div>
	<div class="reveal"><ChallengesLayout /></div>
	</div>
</div>