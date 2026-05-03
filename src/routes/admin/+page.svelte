<script>
	import { onMount } from 'svelte';

	let progressMapComments = {
		UgxJmWrVSNLrkElBfA14AaABAg: { current: 8, goal: 10 },
		UgwqN5F0py4kVtKVfuJ4AaABAg: { current: 3, goal: 10 }
	};

	let progressMapGoals = {};

	let newCommentId = '';
	let newCommentCurrent = 0;
	let newCommentGoal = 10;

	let newGoalId = '';
	let newGoalCurrent = 0;
	let newGoalGoal = 10;

	function saveComments() {
		localStorage.setItem('progressMapComments', JSON.stringify(progressMapComments));
		alert('Challenges saved!');
	}

	function saveGoals() {
		localStorage.setItem('progressMapGoals', JSON.stringify(progressMapGoals));
		alert('Goals saved!');
	}

	function addChallenge() {
		if (!newCommentId) return;
		progressMapComments[newCommentId] = { current: newCommentCurrent, goal: newCommentGoal };
		progressMapComments = { ...progressMapComments };
		newCommentId = '';
		newCommentCurrent = 0;
		newCommentGoal = 10;
	}

	function removeChallenge(id) {
		delete progressMapComments[id];
		progressMapComments = { ...progressMapComments };
	}

	function addGoal() {
		if (!newGoalId) return;
		progressMapGoals[newGoalId] = { current: newGoalCurrent, goal: newGoalGoal };
		progressMapGoals = { ...progressMapGoals };
		newGoalId = '';
		newGoalCurrent = 0;
		newGoalGoal = 10;
	}

	function removeGoal(id) {
		delete progressMapGoals[id];
		progressMapGoals = { ...progressMapGoals };
	}

	onMount(() => {
		const savedComments = localStorage.getItem('progressMapComments');
		if (savedComments) progressMapComments = JSON.parse(savedComments);

		const savedGoals = localStorage.getItem('progressMapGoals');
		if (savedGoals) progressMapGoals = JSON.parse(savedGoals);
	});
</script>

<section class="sm:grid sm:grid-cols-2">
	<div class="p-10">
		<h1 class="font-bebas text-4xl text-white mb-8">CHALLENGES</h1>

		{#each Object.entries(progressMapComments) as [id, progress]}
			<div class="bg-purple-950 p-6 rounded-lg mb-4">
				<h2 class="text-white text-sm mb-2 font-mono">ID: {id}</h2>
				<div class="flex gap-4 items-center flex-wrap">
					<h3 class="text-white text-sm">Current:</h3>
					<input
						type="number"
						bind:value={progress.current}
						class="bg-purple-900 text-white p-1 rounded w-16"
					/>
					<h3 class="text-white text-sm">Goal:</h3>

					<input
						type="number"
						bind:value={progress.goal}
						class="bg-purple-900 text-white p-1 rounded w-16"
					/>
				</div>
				<button
					on:click={() => removeChallenge(id)}
					class="px-4 py-2 bg-red-700 text-white rounded-lg text-sm items-end"
				>
					REMOVE
				</button>
			</div>
		{/each}

		<div class="bg-purple-900 p-6 rounded-lg mb-4 mt-8">
			<h2 class="font-bebas text-2xl text-white mb-4">Add Challenge</h2>
			<div class="flex flex-col gap-3">
				<div class="flex gap-4 items-center flex-wrap">
					<h3 class="text-white text-sm">Comment ID:</h3>
					<input
						type="text"
						bind:value={newCommentId}
						placeholder="UgwqN5F0py..."
						class="bg-purple-900 text-white p-2 rounded flex-1"
					/>
                    </div>
                    				<div class="flex gap-4 items-center flex-wrap">
					<h3 class="text-white text-sm">Current:</h3>
					<input
						type="number"
						bind:value={newCommentCurrent}
						class="bg-purple-900 text-white p-2 rounded w-24"
					/>
					<h3 class="text-white text-sm">Goal:</h3>
					<input
						type="number"
						bind:value={newCommentGoal}
						class="bg-purple-900 text-white p-2 rounded w-24"
					/>
				</div>
				<button
					on:click={addChallenge}
					class="px-6 py-2 bg-purple-600 text-white rounded font-bebas text-xl"
				>
					ADD
				</button>
			</div>
		</div>

		<button
			on:click={saveComments}
			class="mt-4 px-6 py-2 bg-green-700 text-white rounded-lg font-bebas text-xl"
		>
			SAVE ALL
		</button>
	</div>

	<div class="p-10">
		<h1 class="font-bebas text-4xl text-white mb-8">GOALS</h1>

		{#each Object.entries(progressMapGoals) as [id, progress]}
			<div class="bg-purple-950 p-6 rounded-lg mb-4">
				<h2 class="text-white text-sm mb-2 font-mono">ID: {id}</h2>
				<div class="flex gap-4 items-center flex-wrap">
					<h3 class="text-white text-sm">Current:</h3>
					<input
						type="number"
						bind:value={progress.current}
						class="bg-purple-900 text-white p-1 rounded w-16"
					/>
					<h3 class="text-white text-sm">Goal:</h3>
					<input
						type="number"
						bind:value={progress.goal}
						class="bg-purple-900 text-white p-1 rounded w-16"
					/>
					<button
						on:click={() => removeGoal(id)}
						class="px-4 py-2 bg-red-700 text-white rounded-lg text-sm"
					>
						REMOVE
					</button>
				</div>
			</div>
		{/each}

		<div class="bg-purple-900 p-6 rounded-lg mb-4 mt-8">
			<h2 class="font-bebas text-2xl text-white mb-4">Add Goal</h2>
			<div class="flex flex-col gap-3">
				<div class="flex gap-4 items-center flex-wrap">
					<h3 class="text-white text-sm">Goal name:</h3>
					<input
						type="text"
						bind:value={newGoalId}
						placeholder="Do 1000 pushups..."
						class="bg-purple-900 text-white p-2 rounded flex-1"
					/>
				</div>
				<div class="flex gap-4 items-center flex-wrap">
					<h3 class="text-white text-sm">Current:</h3>
					<input
						type="number"
						bind:value={newGoalCurrent}
						class="bg-purple-900 text-white p-2 rounded w-24"
					/>
					<h3 class="text-white text-sm">Goal:</h3>
					<input
						type="number"
						bind:value={newGoalGoal}
						class="bg-purple-900 text-white p-2 rounded w-24"
					/>
				</div>
				<button
					on:click={addGoal}
					class="px-6 py-2 bg-purple-600 text-white rounded font-bebas text-xl"
				>
					ADD
				</button>
			</div>
		</div>

		<button
			on:click={saveGoals}
			class="mt-4 px-6 py-2 bg-green-700 text-white rounded-lg font-bebas text-xl"
		>
			SAVE ALL
		</button>
	</div>
</section>
