<script>
    export let name = "";
    export let logo = ""
    export let followers = 0;
    export let goal = 10000;

    //AI format large number + progress
    const formatNumber = (num) => {
        return num >= 1000 ? (num /1000).toFixed(1) + "K" : num;
    };
    const progress = Math.min((followers / goal) * 100, 100);

</script>
    
    <div class="card bg-gray-800 flex flex-col gap-2 items-center">
        <div><img src={logo} alt="name" class="w-10 h-10 object-contain"/>
            <p class="name">{name}</p>
            <p class="count">{formatNumber(followers)}</p>
            <div class="bar">
                <div class="fill" style="width: {progress}%">

                </div>
            </div>
            <p class="">{formatNumber(followers)} / {formatNumber(goal)}</p>
        </div>
    </div>

    <style>
        .name {
            font-size: 1rem;
            color: white;
        }
        .bar {
            width: 100%;
            height: 8px;
            border-radius: 12px;
            overflow: hidden;
        }
        .fill{
            background: red;
            border-radius: 12px;
        }
        .count {
            font-size: 1rem;
        }
    </style>