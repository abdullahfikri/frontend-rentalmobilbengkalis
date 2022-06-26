<template>
    <div class="p-[100px] w-full bg-blue-100">
        <form @submit.prevent="submitTambahMobil">
            <div>
                <label class="font-semibold" for="jenis">Jenis Mobil</label>
                <select
                    class="ml-8 bg-gray-100 rounded shadow"
                    name="jenis"
                    id="jenis"
                >
                    <option
                        v-for="data in dataJenisMobil"
                        :key="data.id"
                        :value="data.id"
                    >
                        {{ data.nama_mobil }}
                    </option>
                </select>
            </div>
            <div>
                <label class="font-semibold" for="warna">Warna</label>
                <input
                    class="border mt-5 ml-16 bg-gray-100 rounded shadow"
                    type="text"
                    name="warna"
                    id="warna"
                />
            </div>
            <div>
                <label class="font-semibold" for="plat">No. Plat</label>
                <input
                    class="border ml-14 bg-gray-100 rounded shadow mt-5"
                    type="text"
                    maxlength="10"
                    name="plat"
                    id="plat"
                />
            </div>

            <div>
                <label class="font-semibold" for="tahun">Tahun Mobil</label>
                <select
                    class="ml-6 bg-gray-100 rounded shadow mt-5"
                    name="tahun"
                    id="tahun"
                >
                    <option
                        v-for="tahun in tahunMobil"
                        :key="tahun"
                        :value="tahun"
                    >
                        {{ tahun }}
                    </option>
                </select>
            </div>
            <div>
                <label class="font-semibold" for="harga">Harga / Hari</label>
                <input
                    class="ml-6 bg-gray-100 rounded shadow mt-5 mb-4"
                    type="number"
                    name="harga"
                    id="harga"
                />
            </div>
            <div>
                <label class="font-semibold" for="image">Upload Gambar</label>
                <input type="file" name="image" id="image" />
            </div>
            <div>
                <button
                    type="submit"
                    class="py-2 px-4 hover:bg-gray-300 bg-white mt-5 rounded-2xl font-bold"
                >
                    Tambah
                </button>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name: "TambahMobil",
    data() {
        return {
            dataJenisMobil: [],
            tahunMobil: [2022, 2021, 2020, 2019, 2018, 2017, 2016, 2015],
        };
    },
    methods: {
        async getJenisMobil() {
            const response = await fetch(
                `https://rentalmobilbengkalis.000webhostapp.com/rentalmobil/viewjenis_mobil.php`
            );
            const data = await response.json();
            this.dataJenisMobil = data.data;
        },
        async submitTambahMobil(e) {
            const file = e.target[5].files[0];
            const formData = new FormData(e.target);

            if (file !== undefined) {
                formData.append("image", file);
                const response = await fetch(
                    "https://rentalmobilbengkalis.000webhostapp.com/rentalmobil/images/tambahmobil.php",
                    {
                        method: "POST",
                        body: formData,
                    }
                );
                const data = await response.json();
                if (data.status == "sukses") {
                    this.$router.push("/dashboard/mobillist");
                } else {
                    alert("Gagal menambahkan data mobil");
                }
            } else {
                alert("Mohon upload gambar dengan benar");
            }
        },
    },
    created() {
        this.getJenisMobil();
    },
};
</script>

<style></style>
