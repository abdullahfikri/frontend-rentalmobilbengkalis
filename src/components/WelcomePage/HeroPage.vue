<template>
    <div
        class="h-[80vh] bg-blend-normal bg-center bg-no-repeat bg-cover"
        :style="cssBgImg"
    >
        <h1 class="text-4xl font-bold text-white pt-32 pl-32">
            SEWA MOBIL <span class="text-orange-400">BENGKALIS</span>
        </h1>
    </div>
</template>

<script>
export default {
    name: "HeroPage",
    data() {
        return {
            cssBgImg: {
                backgroundImage: `url(${require("@/assets/hero.png")})`,
            },
        };
    },
};
</script>
