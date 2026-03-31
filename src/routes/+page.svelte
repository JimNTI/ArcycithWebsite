<script>
	import Header from '$lib/components/Header.svelte';
	import Hero from '$lib/components/Hero.svelte';
	import SocialMediaShowcase from '$lib/components/SocialMediaShowcase.svelte';
	import pfp from '$lib/images/profilePicture.jpg';

</script>

<svelte:head>
	<title>Arcycith</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<Hero />
<SocialMediaShowcase />

<section id="about_me">

</section>

<section id="goals">
	<div class="goal_card"></div>
</section>
<section id="challenges"></section>
<section id="achievements"></section>




<style>

	#about_me{
		display:flex;
	}

	#goals{
		display:flex;
	}
	#challenges{
		display:flex;
	}
	#achievements{
		display:flex;
	}


</style>
