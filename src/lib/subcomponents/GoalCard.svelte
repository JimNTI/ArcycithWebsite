<script>
    export let text = "";
    export let amount = 0;
    export let current = 0;
    
    const progress = Math.min((current / amount) * 100, 100);

</script>

<div class="flex items-center flex-col h-[auto] m-4 p-2 bg-purple-600 rounded-lg">
    <h3>{text}</h3>
    <div class="flex justify-between w-full">
    <div>{current}</div>
    <div>{amount}</div>
    </div>
    <div class="w-[100%]  bg-purple-400  h-[5px]">
        <div class="h-full bg-white" style="width: {progress}%"></div>
    </div>
</div>