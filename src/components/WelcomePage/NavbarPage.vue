<template>
    <nav class="bg-orange-400 flex items-center justify-center">
        <div class="container text-white p-4 flex justify-between">
            <ul class="flex gap-5 font-bold text-2xl">
                <li>HOME</li>
                <li>ARMADA</li>
                <li>ABOUT</li>
            </ul>
            <button @click="toLogin" class="font-bold text-2xl">LOGIN</button>
        </div>
    </nav>
</template>

<script>
export default {
    name: "NavbarPage",
    methods: {
        toLogin() {
            this.$router.push("/admin");
        },
    },
};
</script>
