<script>
	import { onMount } from 'svelte';
	import CommentCard from '../subcomponents/CommentCard.svelte';

	function decodeHtml(html) {
		const txt = document.createElement('textarea');
		txt.innerHTML = html;
		return txt.value;
	}

	const API_KEY = 'AIzaSyCUhbqBC8aTzQSsBEifGJEB7LGEKE9SxYQ';

	let comments = [];

	onMount(async () => {
		// Load progressMap from localStorage, fall back to defaults
		const saved = localStorage.getItem('progressMapComments');
		const progressMap = saved
			? JSON.parse(saved)
			: {
					UgxJmWrVSNLrkElBfA14AaABAg: { current: 8, goal: 10 },
					UgwqN5F0py4kVtKVfuJ4AaABAg: { current: 3, goal: 10 },
					'UgxGL4tN2-tPiqdnpeJ4AaABAg': { current: 507, goal: 1000 }
				};

		// Load comment IDs from progressMap keys
		const ids = Object.keys(progressMap).join(',');

		const res = await fetch(
			`https://www.googleapis.com/youtube/v3/commentThreads?part=snippet&id=${ids}&key=${API_KEY}`
		);

		const data = await res.json();

		if (data.items) {
			comments = data.items.map((item) => {
				const c = item.snippet.topLevelComment.snippet;
				const p = progressMap[item.id] ?? { current: 0, goal: 0 };
				return {
					pfp: c.authorProfileImageUrl,
					text: decodeHtml(c.textDisplay),
					user: decodeHtml(c.authorDisplayName),
					likes: c.likeCount,
					published: c.publishedAt,
					replies: item.snippet.totalReplyCount,
					link: `https://youtube.com/watch/?v=${c.videoId}&lc=${item.id}`,
					current: p.current,
					goal: p.goal
				};
			});
		}
	});

	//sorting system
	let order = 'asc'; // asc or desc
	let sortBy = 'published'; // published, user, progress

	$: sortedComments = [...comments].sort((a, b) => {
		let valA, valB;

		if (sortBy === 'published') {
			valA = new Date(a.published);
			valB = new Date(b.published);
		} else if (sortBy === 'user') {
			valA = a.user.toLowerCase();
			valB = b.user.toLowerCase();
		} else if (sortBy === 'progress') {
			valA = a.current / a.goal;
			valB = b.current / b.goal;
		}

		if (valA < valB) return order === 'asc' ? -1 : 1;
		if (valA > valB) return order === 'asc' ? 1 : -1;
		return 0;
	});

	let selectedComment = null;
	let open = false;

	function openComment(comment) {
		selectedComment = comment;
		open = true;
	}

	function closeComment() {
		open = false;
		selectedComment = null;
	}
</script>

<section class="m-1 pb-2">
	<h2 class="text-center font-bebas text-4xl">CHALLENGES</h2>
	<div class=" bg-purple-800 sm:m-10 rounded">
		<div class="p-2 flex gap-2 border-4 border-purple-900">
			<select
				bind:value={sortBy}
				class=" m-2 rounded-lg bg-purple-950 text-white outline-black outline"
			>
				<option value="published">Date</option>
				<option value="user">Author</option>
				<option value="progress">Progress %</option>
			</select>

			<button aria-label="Sort order: {order === 'asc' ? 'ascending' : 'descending'}, click to toggle"
				on:click={() => (order = order === 'asc' ? 'desc' : 'asc')}
				class="px-4 m-2 outline outline-black rounded-lg"
			>
				{order === 'asc' ? '↑' : '↓'}
			</button>
		</div>
		{#key sortBy + order}
			<div class="px-4">
				<div
					class="flex flex-row flex-wrap reveal-comments p-1 shadow-[inset_0_4px_10px_rgba(0,0,0,0.8)]"
				>
					{#each sortedComments as comment}
						<CommentCard
							pfp={comment.pfp}
							text={comment.text}
							user={comment.user}
							likes={comment.likes}
							published={comment.published}
							replies={comment.replies}
							link={comment.link}
							current={comment.current}
							goal={comment.goal}
							on:open={() => openComment(comment)}
						/>
					{/each}
				</div>
			</div>
		{/key}
	</div>

	{#if open && selectedComment}
		<div class="fixed inset-0 bg-black/70 flex items-center justify-center z-10 flex-col">
			<div class="bg-white w-[400px] p-6 rounded-xl">
				<div class="flex items-center gap-3">
					<img src={selectedComment.pfp} alt="profile" class="w-10 h-10 rounded-full" />
					<div>
						<p class="text-sm font-semibold text-gray-600">{selectedComment.user}</p>
						<p class="text-xs text-gray-500">{selectedComment.published}</p>
					</div>
				</div>

				<p class="mt-4 text-gray-800">
					{selectedComment.text}
				</p>

				<div class="mt-3 text-sm text-gray-500">
					👍 {selectedComment.likes} 💬 {selectedComment.replies}
				</div>
			</div>
			<button class="px-2 m-2 rounded text-black bg-white" on:click={closeComment}> X </button>
			<a
				href={selectedComment.link}
				target="_blank"
				class="mt-4 block text-center px-4 py-2 bg-red-600 text-white rounded-lg text-sm reveal-button glow-up"
			>
				VIEW ON YOUTUBE
			</a>
		</div>
	{/if}
</section>

<style>
	@keyframes hoverButton {
		from {
			opacity: 0;
			transform: translateY(100px) rotate(270deg);
		}
		to {
			opacity: 1;
			transform: translateY(0px) rotate(360deg);
		}
	}

	.reveal-button {
		animation: hoverButton 1s ease;
	}

	.glow-up {
		transition: transform 1s ease;
	}
	.glow-up:hover {
		transform: translateY(-10px) scale(1.2);
		box-shadow: 0 0 10px 2px rgb(255, 117, 117);
	}
</style>
