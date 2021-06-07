<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <div class="container">
        <b-navbar-brand href="# ">KULINER</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            
            <router-link class="nav-link" to="/">Home</router-link>
            <router-link class="nav-link" to="/foods">Foods</router-link>

          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <ul class="navbar-nav ml-auto">
            <router-link class="nav-link" to="/keranjang">
            CART
            <b-icon-bag></b-icon-bag>
            <span class="badge badge-success ml-2">{{updateKeranjang ? updateKeranjang.length : jumlah_pesanans.length}}</span>
            </router-link>
          </ul>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
  <!-- <div style="margin: 30px">
    <nav class="navbar navbar-expand-lg navbar-light">
      <div class="container">
        <a class="navbar-brand" href="#">KULINER</a>
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav mr-auto">
            <router-link class="nav-link" to="/">Home</router-link>
            <li class="nav-item">
              <router-link class="nav-link" to="/foods">Foods</router-link>
            </li>
          </ul>
          <ul class="navbar-nav ml-auto">
            <router-link class="nav-link" to="/keranjang">
            CART
            <b-icon-bag></b-icon-bag>
            <span class="badge badge-success ml-2">{{updateKeranjang ? updateKeranjang.length : jumlah_pesanans.length}}</span>
            </router-link>
          </ul>
        </div>
      </div>
    </nav>
  </div> -->
</template>

<script>
import axios from "axios";

export default {
  name: "Navbar",
  data() {
    return {
      jumlah_pesanans: [],
    };
  },
  props: ["updateKeranjang"],
  methods: {
    setJumlah(data) {
      this.jumlah_pesanans = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setJumlah(response.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
</style>