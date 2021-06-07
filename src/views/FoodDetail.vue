<template>
  <div class="food-detail">
    <Navbar />
    <div class="container">
      <!-- breadcrumb -->
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link class="text-dark" to="/">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link class="text-dark" to="/foods">Foods</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link class="breadcrumb-item active" to="/foods">
                  Detail Order</router-link
                >
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row">
        <div class="col-md-6">
          <img
            :src="'../assets/pict-product/' + product.gambar"
            class="img-fluid shadow"
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }} </strong>
          </h2>
          <hr />
          <h4>IDR {{ product.harga }}</h4>
          <form class="mt-4" v-on:submit.prevent>
            <!-- v-on:submit.prevent , berfugsi untuk no reload jika diklik button finish   -->
            <div class="mb-3">
              <label for="" class="form-label">Amount</label>
              <input
                type="number"
                class="form-control"
                for="jumlah_pesanan"
                v-model="pesan.jumlah_pesanan"
              />
            </div>
            <div class="mb-3">
              <label for="" class="form-label">Description</label>
              <textarea
                class="form-control"
                for="keterangan"
                v-model="pesan.keterangan"
                placeholder="Food description"
              ></textarea>
            </div>
            <button type="submit" class="btn btn-success" @click="pemesanan">
              <b-icon-cart></b-icon-cart>
              Finish
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
// import Navbar from '../components/Navbar.vue';

import axios from "axios";

export default {
  name: "FoodDetail",
  components: {
    Navbar,
  },
  data() {
    return {
      product: {},
      pesan: {}
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.pesan.jumlah_pesanan) {
        this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs/", this.pesan)
          .then(() => {
            //untuk berpindah ke halaman keranjang
            this.$router.push({ path: "/keranjang" })
            this.$toast.success("Seccess add to cart !", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((error) => console.log(error));
      } else {
        this.$toast.error("Failed add to cart !", {
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
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>