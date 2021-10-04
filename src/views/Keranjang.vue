<template>
    <div class="keranjang">
        <Navbar :updateKeranjang="keranjangs" />
        <div class="container">
            <div class="row mt-4">
                <div class="col">
                    <nav aria-label="breadcrumb">
                        <ol class="breadcrumb">
                            <li class="breadcrumb-item">
                                <router-link to="/" class="text-dark"
                                    >Home</router-link
                                >
                            </li>
                            <li class="breadcrumb-item">
                                <router-link to="/foods" class="text-dark"
                                    >Foods</router-link
                                >
                            </li>
                            <li
                                class="breadcrumb-item active"
                                aria-current="page"
                            >
                                Keranjang
                            </li>
                        </ol>
                    </nav>
                </div>
            </div>
            <div class="row">
                <div class="col">
                    <h2>Keranjang <strong>Saya</strong></h2>
                    <div class="table-responsive mt-3">
                        <table class="table table-striped">
                            <thead>
                                <tr>
                                    <th scope="col">#</th>
                                    <th scope="col">Foto</th>
                                    <th scope="col">Makanan</th>
                                    <th scope="col">Keterangan</th>
                                    <th scope="col">Jumlah</th>
                                    <th scope="col">Harga</th>
                                    <th scope="col">Total Harga</th>
                                    <th scope="col">Hapus</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr
                                    v-for="(keranjang, i) in keranjangs"
                                    :key="keranjang.id"
                                >
                                    <th scope="row">{{ i + 1 }}</th>
                                    <td>
                                        <img
                                            :src="
                                                '/assets/images/' +
                                                keranjang.product.gambar
                                            "
                                            alt="gambar"
                                            class="img-fluid shadow"
                                            width="200"
                                        />
                                    </td>
                                    <td>
                                        <strong>{{
                                            keranjang.product.nama
                                        }}</strong>
                                    </td>
                                    <td>{{ keranjang.keterangan || "-" }}</td>
                                    <td>{{ keranjang.jumlah_pemesanan }}</td>
                                    <td>Rp. {{ keranjang.product.harga }}</td>
                                    <td>
                                        <strong>
                                            Rp.
                                            {{
                                                keranjang.product.harga *
                                                keranjang.jumlah_pemesanan
                                            }}
                                        </strong>
                                    </td>
                                    <td align="center">
                                        <button
                                            class="btn btn-danger btn-sm"
                                            @click="
                                                hapusKeranjangs(keranjang.id, i)
                                            "
                                        >
                                            <b-icon-trash></b-icon-trash>
                                        </button>
                                    </td>
                                </tr>
                            </tbody>
                            <tfoot>
                                <tr>
                                    <td colspan="6" align="right">
                                        <strong>Total harga</strong>
                                    </td>
                                    <td>
                                        <strong>Rp. {{ totalHarga }}</strong>
                                    </td>
                                </tr>
                            </tfoot>
                        </table>
                    </div>
                </div>
            </div>
            <div class="row justify-content-end">
                <div class="col-md-4">
                    <form class="mt-4" v-on:submit.prevent>
                        <div class="form-group">
                            <label for="nama">Nama</label>
                            <input
                                type="text"
                                class="form-control"
                                id="nama"
                                v-model="pesan.nama"
                            />
                        </div>
                        <div class="form-group">
                            <label for="no_meja">Nomor Meja</label>
                            <input
                                type="number"
                                min="1"
                                class="form-control"
                                id="no_meja"
                                v-model="pesan.no_meja"
                            />
                        </div>
                        <button
                            type="submit"
                            class="btn btn-success float-right"
                            @click="checkout"
                        >
                            <b-icon-cart></b-icon-cart> Pesan
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
    name: "Keranjang",
    components: {
        Navbar,
    },
    data() {
        return {
            keranjangs: [],
            pesan: {},
        };
    },
    methods: {
        setKeranjangs(data) {
            this.keranjangs = data;
        },
        hapusKeranjangs(id, i) {
            axios
                .delete("http://localhost:3000/keranjangs/" + id)
                .then(() =>
                    this.$toast.error("Sukses hapus keranjang", {
                        type: "error",
                        position: "top-right",
                        duration: 3000,
                        dismissible: true,
                    })
                )
                .catch((error) => console.log(error));
            this.keranjangs.splice(i, 1);
        },
        checkout() {
            if (this.pesan.nama && this.pesan.no_meja) {
                this.pesan.keranjangs = this.keranjangs;
                axios
                    .post("http://localhost:3000/pesanans", this.pesan)
                    .then(() => {
                        this.keranjangs.map((item) => {
                            axios
                                .delete(
                                    "http://localhost:3000/keranjangs/" +
                                        item.id
                                )
                                .catch((error) => console.log(error));
                        });
                        this.$router.push({ path: "/pesanan-sukses" });
                        this.$toast.success("Makanan sukses dipesan !", {
                            type: "success",
                            position: "top-right",
                            duration: 3000,
                            dismissible: true,
                        });
                    })
                    .catch((err) => console.log(err));
            } else {
                this.$toast.error("Nama dan Nomor Meja harus diisi !", {
                    type: "error",
                    position: "top-right",
                    duration: 3000,
                    dismissible: true,
                });
            }
        },
    },
    mounted() {
        axios
            .get("http://localhost:3000/keranjangs")
            .then((response) => this.setKeranjangs(response.data))
            .catch((error) => console.log(error));
    },
    computed: {
        totalHarga() {
            return this.keranjangs.reduce(
                (total, data) =>
                    total + data.product.harga * data.jumlah_pemesanan,
                0
            );
        },
    },
};
</script>

<style>
</style>