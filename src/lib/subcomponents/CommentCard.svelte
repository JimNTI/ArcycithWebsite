<script>
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

	export let pfp = '';
	export let text = '';
	export let user = '';
	export let likes = 0;
	export let link = '';
	export let current = 0;
	export let goal = 0;
	export let published = '';
	export let replies = 0;

    function timeAgo(dateStr) {
		const diff = Date.now() - new Date(dateStr).getTime();
		const mins = Math.floor(diff / 60000);
		const hours = Math.floor(mins / 60);
		const days = Math.floor(hours / 24);
		const weeks = Math.floor(days / 7);
		const months = Math.floor(days / 30);
		const years = Math.floor(days / 365);
		if (mins < 1) return 'just now';
		if (mins < 60) return `${mins}m ago`;
		if (hours < 24) return `${hours}h ago`;
		if (days < 7) return `${days}d ago`;
		if (weeks < 5) return `${weeks}w ago`;
		if (months < 12) return `${months}mo ago`;
		return `${years}y ago`;
	}

	let open = false;

	const progress = Math.min((current / goal) * 100, 100);
</script>

<button
	on:click={() => dispatch('open')}
	class="cursor-pointer flex flex-row h-[auto] m-4 p-3 bg-white rounded-sm"
>
	<div class="flex flex-col w-full px-3">
		<div class="flex gap-2">
			<img src={pfp} alt="profile" class="h-10 w-10 rounded-full" />
			<div class="flex flex-col">
				<h3 class="text-sm font-semibold">{user}</h3>
				<p class="text-xs text-gray-50 text-start">{timeAgo(published)}</p>
			</div>
		</div>

		<p class="text-gray-800 mt-1">{text}</p>

		<div class="flex gap-4 mt-1">
			<span>👍{likes}</span>
			<span>💬{replies}</span>
		</div>
		{#if goal > 0}
			<div class="mt-1 mb-1">
				<div class="flex justify-between text-xs text-gray-500 mb-1">
					<span>Progress</span>
					<span>{progress}%</span>
				</div>
				<div class="w-full h-1.5 bg-gray-200 rounded-full overflow-hidden">
					<div class="h-full bg-purple-600 rounded-full" style="width: {progress}%"></div>
				</div>
			</div>
		{/if}
	</div>
</button>

<style>
	* {
		color: black;
	}
</style>
