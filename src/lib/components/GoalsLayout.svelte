<script>
	import GoalCard from '../subcomponents/GoalCard.svelte';
	const allGoals = [
		{ text: 'Do 1000 Pushups', amount: 1000, current: 103 },
		{ text: 'Do 1000 Pushups', amount: 1000, current: 103 },
		{ text: 'Meet 100 Fans', amount: 100, current: 100 },
		{ text: 'Meet 100 Fans', amount: 100, current: 100 }
	];
	$: completedGoals = allGoals.filter((g) => g.current >= g.amount);
	$: progressGoals = allGoals.filter((g) => g.current < g.amount);
</script>

<section class="p-8 sm:p-10">
<div class="sm:grid sm:grid-cols-2">
	<div>
		<h2 class="text-center font-bebas text-4xl">GOALS COMPLETED</h2>
		<div class="fade-in">
			{#each completedGoals as goal}
				<GoalCard text={goal.text} amount={goal.amount} current={goal.current} />
			{/each}
		</div>
	</div>

	<div>
		<h2 class="text-center font-bebas text-4xl">IN PROGRESS</h2>
		<div>
			{#each progressGoals as goal}
				<GoalCard text={goal.text} amount={goal.amount} current={goal.current} />
			{/each}
		</div>
	</div>
    </div>
</section>
