<template>
    <div class="w-[300px] border flex flex-col border-gray-500 font-serif">
        <div>
            <p class="ml-5">
                No. <span>{{ nomor + 1 }}</span>
            </p>
        </div>
        <p class="ml-5">
            Nama:
            <button class="text-gray-500" @click="goPelanggan">
                {{ data.nama }}
            </button>
        </p>
        <p class="ml-5">
            Alamat: <span> {{ data.alamat }}</span>
        </p>
        <p class="ml-5">
            Tanggal Pinjam: <span>{{ data.tanggal_pinjam }}</span>
        </p>
        <!-- tgl kembali -->
        <p class="ml-5">
            Tanggal Kembali: <span>{{ data.tanggal_kembali }}</span>
        </p>
        <!-- mobil -->
        <p class="ml-5">
            Mobi: <span>{{ data.nama_mobil }}</span>
        </p>
        <!-- plat -->
        <p class="ml-5">
            Plat: <span>{{ data.plat }}</span>
        </p>
        <!-- harga -->
        <p class="ml-5">
            Total Harga: <span>{{ data.harga }}</span>
        </p>
        <!-- status -->
        <p class="ml-5">{{ statusTransaksi == 0 ? "Selesai" : "Aktif" }}</p>
        <!-- no telp -->
        <p class="ml-5">
            No. Telp <span>{{ data.nomor_telp }}</span>
        </p>
        <button
            @click="onSelesaiClick"
            class="bg-gray-400 hover:bg-gray-500"
            v-if="data.status == 1"
        >
            Selesai
        </button>
    </div>
</template>

<script>
export default {
    name: "CardTransaksi",
    data() {
        return {
            statusTransaksi: this.data.status,
            idPelanggan: this.data.id_pelanggan,
            idMobil: this.data.id_mobil,
            idTransaksi: this.data.id_transaksi,
        };
    },
    props: ["nomor", "data"],
    methods: {
        goPelanggan() {
            this.$router.push(`/dashboard/pelanggan/${this.idPelanggan}`);
        },
        async onSelesaiClick() {
            const response = await fetch(
                `https://rentalmobilbengkalis.000webhostapp.com/rentalmobil/selesaikantransaksi.php?id=${this.idTransaksi}&idmobil=${this.idMobil}`
            );

            const dataResponse = await response.json();
            if (dataResponse.status === "sukses") {
                this.statusTransaksi = 0;
                this.$router.go();
            } else {
                alert("Gagal menyelesaikan transaksi");
            }
        },
    },
};
</script>

<style></style>
