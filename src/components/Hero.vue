<template>
    <div class="hero">
        <!-- Desktop -->
        <div class="d-md-block d-none">
            <div class="row mt-2">
                <div class="col-md-6">
                    <div class="d-flex h-100">
                        <div class="justify-content-center align-self-center">
                            <h2>
                                <strong>Delicious Food Menu, </strong><br />
                                in Your Gadget
                            </h2>
                            <p>
                                Ayo segera pilih dan pesan makanan favorit anda.
                            </p>
                            <router-link
                                class="btn btn-lg btn-success"
                                to="/foods"
                            >
                                <b-icon-arrow-right></b-icon-arrow-right>
                                Pesan
                            </router-link>
                        </div>
                    </div>
                </div>
                <div class="col-md-6">
                    <img
                        src="/assets/images/hero.png"
                        alt="hero"
                        width="100%"
                    />
                </div>
            </div>
        </div>

        <!-- Mobile  -->
        <div class="d-sm-block d-md-none">
            <div class="row mt-2">
                <div class="col-md-6">
                    <img
                        src="../../public/assets/images/hero.png"
                        alt="hero"
                        width="100%"
                    />
                </div>
                <div class="col-md-6 mt-2">
                    <div class="d-flex h-100">
                        <div class="justify-content-center align-self-center">
                            <h2>
                                <strong>Delicious Food Menu, </strong><br />
                                in Your Gadget
                            </h2>
                            <p>
                                Ayo segera pilih dan pesan makanan favorit anda.
                            </p>
                            <router-link
                                class="btn btn-lg btn-success"
                                to="/foods"
                            >
                                <b-icon-arrow-right></b-icon-arrow-right>
                                Pesan
                            </router-link>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Hero",
};
</script>

<style>
</style>