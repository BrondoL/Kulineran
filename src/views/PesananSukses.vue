<template>
    <div class="pesanan-sukses">
        <Navbar :sukses="true" />
        <div class="container">
            <div class="row justify-content-center mt-5">
                <div class="col text-center">
                    <img
                        src="/assets/images/menunggu.png"
                        alt="menunggu"
                        width="300"
                    />
                    <h2><strong>Sukses!!</strong></h2>
                    <h4>
                        Pesanan anda segera diproses <br />
                        Selamat menunggu !
                    </h4>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
export default {
    name: "PesananSukses",
    components: {
        Navbar,
    },
};
</script>

<style>
</style>