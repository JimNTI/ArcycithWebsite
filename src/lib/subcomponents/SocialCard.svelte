<script>
	export let link = '';
	export let name = '';
	export let logo = '';
	export let followers = 0;
	export let goal = 10000;

	//AI format large number + progress
	const formatNumber = (num) => {
		return num >= 1000 ? (num / 1000).toFixed(1) + 'K' : num;
	};
	$: progress = Math.min((followers / goal) * 100, 100);
</script>

<div class="flex flex-col items-center social-container relative z-1">
	<a
		href={link}
		target="_blank"
		class="card flex flex-col items-center outline p-4 rounded-lg "
	>
		<div class="flex items-end h-10 z-[-1]">
			<img src={logo} alt="name" class="object-contain h-10 relative p-1 justify-end logo-animation" />
		</div>
	</a>

	<div class="w-[80%]">
		<div class="bar">
			<div class="fill bg-red-400" style="width: {progress}%"></div>
		</div>
	</div>
    	<div class="flex justify-between w-[80%]">
		<div class="text-[10px] p-1 font-bold">{formatNumber(followers)}</div>

		<div class="text-[10px] p-1 font-bold">{formatNumber(goal)}</div>
	</div>
</div>

<style>
	.bar {
		display: flex;
		align-items: center;
		width: 100%;
		height: 12px;
		border-radius: 12px;
		overflow: hidden;
		border-width: 2px;
		border-color: purple;
		background: #2b2b2b;
	}
	.fill {
		background: linear-gradient(to right, purple, purple);
		height: 80%;
		border-radius: 12px;
		transition: width 0.5s ease;
		margin: 1px;
	}

	@keyframes logoAnimation{
    from { opacity: 0; transform: translateY(40px) scale(0.8) rotate(180deg);}
    to {opacity: 1; transform: translateY(0px) scale(1) rotate(360deg);}
	}

	.social-container:hover .logo-animation {
		animation: logoAnimation 0.5s ease
	}
</style>
