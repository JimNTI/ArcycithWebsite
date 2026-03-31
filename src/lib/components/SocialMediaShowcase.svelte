<script>
    import SocialCard from "../subcomponents/SocialCard.svelte"

    const socials = [
        {link: "https://instagram.com/arcycith/",
        name: "Instagram",
        logo: "images/instagram.png",
        followers: 74000,
        goal: 100000
        },
        {link: "https://youtube.com/@Arcycith",
        name: "Youtube",
        logo: "images/youtube.png",
        followers: 42331,
        goal: 50000
        },
        {link: "https://tiktok.com/@Arcycith",
        name: "TikTok",
        logo: "images/tiktok.png",
        followers: 1063,
        goal: 10000
        },
        {link: "https://twitch.com/@Arcycith",
        name: "Twitch",
        logo: "images/twitch.png",
        followers: 1063,
        goal: 10000
        }
    ]
</script>
<section class="flex items-center flex-col">
    <h1 class="text-center p-1 font-bold">ARCYCITH</h1>

    <div class="grid grid-cols-4 gap-6 p-4 w-[400px]">
    {#each socials as social}
        <SocialCard
            link={social.link}
            name={social.name}
            logo={social.logo}
            followers={social.followers}
            goal={social.goal}
        />
    {/each}
    </div>
    <button class="bg-purple-600 rounded-md p-1 shadow-[0_2px_4px_rgba(0,0,0,2)]">MORE SOCIALS</button>
</section>