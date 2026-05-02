<script>
	import SocialCard from "../subcomponents/SocialCard.svelte"
	const socials = [
		{ link: "https://instagram.com/arcycith/", name: "Instagram", logo: "images/instagram.png", followers: 74000, goal: 100000 },
		{ link: "https://youtube.com/@Arcycith", name: "Youtube", logo: "images/youtube.png", followers: 42331, goal: 50000 },
		{ link: "https://tiktok.com/@Arcycith", name: "TikTok", logo: "images/tiktok.png", followers: 1063, goal: 10000 },
		{ link: "https://twitch.com/@Arcycith", name: "Twitch", logo: "images/twitch.png", followers: 1063, goal: 10000 },
		{ link: "https://www.roblox.com/users/493377109/profile", name: "Roblox", logo: "images/roblox.png", followers: 1063, goal: 10000 },
		{ link: "https://discord.gg/KWY93cA4W6", name: "Discord", logo: "images/discord.png", followers: 1063, goal: 10000 }
	]
</script>

<section class="flex flex-col items-center py-2 px-4">
	<h3 class="text-center text-s tracking-widest font-medium mb-1" style="color: #7f77dd;">ARCYCITH</h3>
	<h2 class="text-center text-sm mb-8 bg-clip-text text-transparent bg-gradient-to-r from-pink-500 to-violet-500">Content Creator</h2>
	<div class="grid grid-cols-4 sm:grid-cols-6 sm:gap-6 gap-4 w-full max-w-lg sm:max-w-xl">
		{#each socials as social}
			<SocialCard link={social.link} name={social.name} logo={social.logo} followers={social.followers} goal={social.goal} />
		{/each}
	</div>
	<button class="mt-8 px-6 py-2 rounded-md text-xs tracking-widest font-medium transition-all" style="background: rgba(127,119,221,0.12); border: 0.5px solid rgba(127,119,221,0.4); color: #afa9ec;">
		MORE SOCIALS
	</button>
</section>