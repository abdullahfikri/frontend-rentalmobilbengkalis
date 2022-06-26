<template>
    <div class="border w-80 flex flex-col rounded-xl overflow-hidden">
        <img
            class="h-[200px] w-full bg-slate-100"
            :src="data.url_image"
            alt="contoh"
        />
        <div class="py-6 text-center border-t">
            <h1 class="font-bold text-3xl text-white">{{ data.jenis }}</h1>
            <p class="font-bold text-lg bg-white py-2">{{ data.tahun }}</p>
            <p class="text-xl text-white">{{ idrFormat }}/Hari</p>
            <p
                :class="
                    data.status == 0
                        ? 'text-green-700 font-bold bg-white py-1 text-lg'
                        : 'text-red-500 font-bold bg-white py-1 text-lg'
                "
            >
                {{ status }}
            </p>
        </div>
    </div>
</template>

<script>
export default {
    name: "CardPage",
    data() {
        return {
            idrFormat: null,
            status: "",
        };
    },
    props: ["data"],
    methods: {
        convertToIdrFormat() {
            this.idrFormat = new Intl.NumberFormat("id-ID", {
                style: "currency",
                currency: "IDR",
            }).format(this.data.harga);
        },
        checkStatus() {
            if (this.data.status == 1) {
                this.status = "Sedang Disewa";
            } else {
                this.status = "Tersedia";
            }
        },
    },
    created() {
        this.convertToIdrFormat();
        this.checkStatus();
    },
};
</script>

<style></style>
