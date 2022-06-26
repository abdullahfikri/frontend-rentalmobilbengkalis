<template>
    <div class="p-20 w-fit bg-blue-100">
        <h1 class="mb-7 font-bold text-center text-2xl">Daftar pelanggan</h1>
        <div class="flex flex-wrap">
            <CardTransaksi
                v-for="(data, index) in dataFetchPelanggan"
                :key="data.id_transaksi"
                :nomor="index"
                :data="data"
            />
        </div>
    </div>
</template>

<script>
import CardTransaksi from "./CardTransaksi.vue";
export default {
    components: {
        CardTransaksi,
    },
    name: "PelangganPage",
    data() {
        return {
            dataFetchPelanggan: {},
        };
    },
    methods: {
        async onFetchData() {
            try {
                const response = await fetch(
                    "https://rentalmobilbengkalis.000webhostapp.com/rentalmobil/viewtransaksi.php"
                );

                const data = await response.json();
                this.dataFetchPelanggan = data.data;
            } catch (err) {
                alert(err.message);
            }
        },
    },
    created() {
        this.onFetchData();
    },
};
</script>

<style></style>
