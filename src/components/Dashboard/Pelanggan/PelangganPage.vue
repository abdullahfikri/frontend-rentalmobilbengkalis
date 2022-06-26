<template>
    <div class="p-20 bg-blue-100 w-full">
        <div class="font-serif">
            <h2 class="font-bold text-2xl mb-4">Profil</h2>
            <img
                :src="dataPelanggan.url_image"
                alt="image_person"
                class="mt-3 float-left mr-10 w-[225px] h-[225px]"
            />

            <p class="mt-10">Nama : {{ dataPelanggan.nama }}</p>
            <p class="mt-3">Kelamin : {{ dataPelanggan.kelamin }}</p>
            <p class="mt-3">No. KTP : {{ dataPelanggan.nik }}</p>
            <p class="mt-3">No. Telp : {{ dataPelanggan.nomor_telp }}</p>
            <p class="mt-3">Alamat : {{ dataPelanggan.alamat }}</p>
        </div>
        <button
            @click="goBack"
            class="mb-3 py-2 px-4 bg-gray-400 hover:bg-gray-500 mt-10 rounded-2xl font-serif"
        >
            Back
        </button>
        <button
            @click="deletePelanggan"
            class="ml-2 mb-3 py-2 px-4 bg-gray-400 hover:bg-gray-500 rounded-2xl font-serif"
        >
            Delete Pelanggan
        </button>
    </div>
</template>

<script>
export default {
    name: "PelangganPage",
    data() {
        return {
            idPelanggan: this.$route.params.id,
            dataPelanggan: {},
        };
    },
    methods: {
        async fetchDataPelanggan(id) {
            const response = await fetch(
                `https://rentalmobilbengkalis.000webhostapp.com/rentalmobil/viewpelanggan.php?id=${id}`
            );
            const data = await response.json();
            this.dataPelanggan = data.data;
        },
        async deletePelanggan() {
            if (
                window.confirm(
                    "Apakah anda yakin ingin menghapus pelanggan ini?"
                )
            ) {
                const response = await fetch(
                    `https://rentalmobilbengkalis.000webhostapp.com/rentalmobil/deletepelanggan.php?id=${this.idPelanggan}`
                );
                const dataResponse = await response.json();
                if (dataResponse.status === "sukses") {
                    this.$router.push("/dashboard/pelanggan");
                } else {
                    alert("Gagal menghapus user");
                }
            }
        },
        goBack() {
            this.$router.back();
        },
    },
    created() {
        this.fetchDataPelanggan(this.idPelanggan);
    },
};
</script>

<style></style>
