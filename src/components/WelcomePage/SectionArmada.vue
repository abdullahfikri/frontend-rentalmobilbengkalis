<template>
    <div class="bg-teal-700 flex items-center flex-col">
        <div class="bg-white w-full">
            <h1 class="font-bold text-3xl text-center py-10">
                Armada Rental Bengkalis
            </h1>
        </div>
        <div class="py-10 gap-5 container flex flex-wrap justify-center">
            <ArmadaCard v-for="data in dataMobil" :key="data.id" :data="data" />
        </div>
    </div>
</template>

<script>
import ArmadaCard from "./ArmadaCard.vue";
export default {
    components: { ArmadaCard },
    data() {
        return {
            dataMobil: [],
        };
    },
    methods: {
        async getMobil() {
            const response = await fetch(
                "https://rentalmobilbengkalis.000webhostapp.com/rentalmobil/viewmobil.php"
            );
            const data = await response.json();
            this.dataMobil = data.data;
        },
        toTambahMobil() {
            this.$router.push("/dashboard/tambahmobil");
        },
    },
    created() {
        this.getMobil();
    },
};
</script>

<style></style>
