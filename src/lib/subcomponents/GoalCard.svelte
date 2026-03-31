<script>
    export let text = "";
    export let amount = 0;
    export let current = 0;
    
    const progress = Math.min((current / amount) * 100, 100);

</script>

<div class="flex items-center flex-col m-8 h-[70px] bg-purple-600 rounded-lg">
    <h2>{text}</h2>
    <div class="flex justify-between w-full">
    <div>{current}</div>
    <div>{amount}</div>
    </div>
    <div class="w-[80%] bg-white h-[5px]">
        <div class="h-full  bg-purple-400" style="width: {progress}%"></div>
    </div>
</div>