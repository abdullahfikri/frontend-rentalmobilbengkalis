<template>
    <div class="bg-sky-700">
        <main class="form-signin grid place-items-center h-screen">
            <div class="border p-[50px] bg-blue-100">
                <form @submit.prevent="onSubmit">
                    <h1
                        class="text-center font-bold font-serif pb-2 mb-3 text-2xl"
                    >
                        LOGIN
                    </h1>

                    <div class="form-floating">
                        <input
                            type="text"
                            id="user"
                            placeholder="Username"
                            v-model="username"
                            class="form-control shadow p-[10px] w-[250px]"
                        />
                    </div>
                    <div class="form-floating">
                        <input
                            id="password"
                            v-model="password"
                            placeholder="Password"
                            type="password"
                            class="form-control shadow p-[10px] w-[250px] mt-2"
                        />
                    </div>

                    <button
                        class="bg-sky-700 hover:bg-sky-900 p-[10px] font-bold text-white w-full mt-5 rounded shadow"
                        type="submit"
                    >
                        Login
                    </button>
                </form>
            </div>
        </main>
    </div>
</template>

<script>
export default {
    name: "LoginPage",
    data() {
        return {
            username: "",
            password: "",
        };
    },
    methods: {
        async onSubmit() {
            try {
                const response = await fetch(
                    `https://rentalmobilbengkalis.000webhostapp.com/rentalmobil/login.php?username=${this.username}&password=${this.password}`,
                    {
                        mode: "cors",
                    }
                );

                if (!response.ok)
                    throw new Error("Problem fetching data from server");

                const data = await response.json();
                if (data.status === "sukses") {
                    localStorage.setItem("login", "1");
                    this.$router.push("/dashboard/pelanggan");
                } else {
                    alert(data.message);
                }
            } catch (err) {
                alert(err.message);
            }
        },
    },
    created() {
        if (localStorage.getItem("login") === "1") {
            this.$router.push("/dashboard/pelanggan");
        }
    },
};
</script>
