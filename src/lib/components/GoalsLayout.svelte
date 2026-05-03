<script>
    import { onMount } from 'svelte';
	import GoalCard from '../subcomponents/GoalCard.svelte';
	let allGoals = [
	];
	$: completedGoals = allGoals.filter((g) => g.current >= g.amount);
	$: progressGoals = allGoals.filter((g) => g.current < g.amount);


  onMount(() => {
    const saved = localStorage.getItem('progressMapGoals');
    if (saved) {
      const parsed = JSON.parse(saved);
      // convert from {id: {current, goal}} to [{text, amount, current}]
      allGoals = Object.entries(parsed).map(([text, values]) => ({
        text,
        amount: values.goal,
        current: values.current
      }));
    }
  });
</script>

<section class="p-8 sm:p-10">
<div class="sm:grid sm:grid-cols-2">
	<div class="sm:order-2">
		<h2 class="text-center font-bebas text-4xl">GOALS COMPLETED</h2>
		<div class="fade-in max-h-[300px] overflow-y-auto no-scrollbar">
			{#each completedGoals as goal}
				<GoalCard text={goal.text} amount={goal.amount} current={goal.current} />
			{/each}
		</div>
	</div>

	<div class="sm:order-1">
		<h2 class="text-center font-bebas text-4xl">IN PROGRESS</h2>
		<div class="max-h-[300px] overflow-y-auto no-scrollbar">
			{#each progressGoals as goal}
				<GoalCard text={goal.text} amount={goal.amount} current={goal.current} />
			{/each}
		</div>
	</div>
    </div>
</section>
