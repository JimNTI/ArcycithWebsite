<script>
  import GoalCard from "../subcomponents/GoalCard.svelte"
const allGoals = [
        {text: "Do 1000 Pushups",
        amount: 1000,
        current: 103,
        },
        {text: "Meet 100 Fans",
        amount: 100,
        current: 100,
        }
    ]
    $: completedGoals = allGoals.filter(g => g.current >= g.amount)
    $: progressGoals = allGoals.filter(g => g.current < g.amount)
</script>

<section>
    <div>
    <h1 class="text-center">GOALS COMPLETED</h1>
        <div>
        {#each completedGoals as goal}
            <GoalCard
                text={goal.text}
                amount={goal.amount}
                current={goal.current}
            />
        {/each}
        </div>
    </div>

    <div>
    <h1 class="text-center">IN PROGRESS</h1>
    <div>
        {#each progressGoals as goal}
            <GoalCard
                goal_text={goal.text}
                amount={goal.amount}
                current={goal.current}
            />
        {/each}
    </div>
    </div>
</section>