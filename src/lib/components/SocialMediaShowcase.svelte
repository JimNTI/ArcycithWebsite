<script>
    import SocialCard from "../subcomponents/SocialCard.svelte"
    import youtube from '../images/youtube.png';
    import instagram from '../images/instagram.png';
    const socials = [
        {name: "Instagram",
        logo: "/images/instagram.png",
        followers: 1000,
        goal: 10000

        },
        {name: "Youtube",
        logo: "/images/youtube.png",
        followers: 1063,
        goal: 10000
        }
    ]
</script>
<section>
    <div class="grid grid-cols-4 gap-4">
    {#each socials as social}
        <SocialCard
            name={social.name}
            logo={social.logo}
            followers={social.followers}
            goal={social.goal}
        />
    {/each}
    </div>
</section>