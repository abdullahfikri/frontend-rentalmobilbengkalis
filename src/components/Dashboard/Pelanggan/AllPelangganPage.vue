<template>
    <div class="p-52 w-full bg-blue-100 h-full container">
        <h1 class="mb-4 font-bold text-2xl py-5 text-center">
            Daftar pelanggan
        </h1>

        <div class="flex flex-wrap gap-2 font-serif">
            <CardPelanggan
                v-for="(dataPelanggan, index) in data"
                :key="dataPelanggan.id_transaksi"
                :nomor="index"
                :data="dataPelanggan"
            />
        </div>
    </div>
</template>

<script>
// import AllPelangganRowVue from "./AllPelangganRow.vue";
import CardPelanggan from "./CardPelanggan.vue";
export default {
    components: { CardPelanggan },
    name: "AllPelanggan",
    data() {
        return {
            data: [],
        };
    },
    methods: {
        async fetchDataViewPelanggan() {
            const response = await fetch(
                "https://rentalmobilbengkalis.000webhostapp.com/rentalmobil/viewallpelanggan.php"
            );

            const dataResponse = await response.json();
            this.data = dataResponse.data;
        },
    },
    created() {
        this.fetchDataViewPelanggan();
    },
};
</script>

<style></style>
