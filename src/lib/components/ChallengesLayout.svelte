<script>
	import { onMount } from 'svelte';
	import CommentCard from '../subcomponents/CommentCard.svelte';

	function decodeHtml(html) {
		const txt = document.createElement('textarea');
		txt.innerHTML = html;
		return txt.value;
	}

	const API_KEY = 'AIzaSyCUhbqBC8aTzQSsBEifGJEB7LGEKE9SxYQ';

	const commentsIds = [
		'UgxJmWrVSNLrkElBfA14AaABAg',
		'UgwqN5F0py4kVtKVfuJ4AaABAg',
		'UgxGL4tN2-tPiqdnpeJ4AaABAg'
	];

	const progressMap = {
		UgxJmWrVSNLrkElBfA14AaABAg: { current: 8, goal: 10 },
		UgwqN5F0py4kVtKVfuJ4AaABAg: { current: 3, goal: 10 },
		'UgxGL4tN2-tPiqdnpeJ4AaABAg': { current: 507, goal: 1000 }
	};

	let comments = [];

	onMount(async () => {
		const ids = commentsIds.join(',');
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
	<div>
		<div class="m-10 bg-purple-800 rounded-lg h-full">
			<div class="p-2 flex item-end">
				<button class="p-2 m-2 outline rounded-lg">List</button>
				<button class="p-2 m-2 outline rounded-lg">Modes</button>
			</div>
			<div class="flex flex-row flex-wrap">
				{#each comments as comment}
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
	</div>

	{#if open && selectedComment}
		<div class="fixed inset-0 bg-black/70 flex items-center justify-center z-10">
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
			<button class="p-2" on:click={closeComment}> X </button>
		</div>
	{/if}
</section>
