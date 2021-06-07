<template>
  <div class="keranjang">
    <Navbar :updateKeranjang="keranjangs" />
    <div class="container">
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
                <router-link class="breadcrumb-item active" to="/keranjang">
                  Cart</router-link
                >
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row mt-4">
        <div class="col">
          <h2>My <strong>Cart</strong></h2>
        </div>
        <div class="table-responsive mt-3">
          <table class="table">
            <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Pict</th>
                <th scope="col">Food</th>
                <th scope="col">Desc</th>
                <th scope="col">Amount</th>
                <th scope="col">Price</th>
                <th scope="col">Total</th>
                <th scope="col">Action</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(keranjang, index) in keranjangs" :key="keranjang.id">
                <th>{{ index + 1 }}</th>
                <td>
                  <img
                    :src="'../assets/pict-product/' + keranjang.products.gambar"
                    class="img-fluid shadow"
                    width="205"
                  />
                </td>
                <td>{{ keranjang.products.nama }}</td>
                <td>{{ keranjang.keterangan ? keranjang.keterangan : "-" }}</td>
                <td align="center">{{ keranjang.jumlah_pesanan }}</td>
                <td>IDR {{ keranjang.products.harga }}</td>
                <td>
                  IDR {{ keranjang.products.harga * keranjang.jumlah_pesanan }}
                </td>
                <td align="center" class="text-danger">
                  <b-icon-trash
                    @click="hapusKeranjangs(keranjang.id)"
                  ></b-icon-trash>
                </td>
              </tr>
              <tr>
                <td colspan="6" align="right">
                  <strong>Grand Total :</strong>
                </td>
                <td>IDR {{ totalHarga }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
    <div class="row justify-content-end">
      <div class="col">

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
    };
  },
  methods: {
    setKeranjangs(data) {
      this.keranjangs = data;
    },
    hapusKeranjangs(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        .then(() => {
          this.$toast.error(" Data Cart Deleted !", {
            type: "error",
            position: "top-right",
            duration: 3000,
            dismissible: true,
          });
          //untutk no-reload jika data dihapus
          axios
            .get("http://localhost:3000/keranjangs/")
            .then((response) => this.setKeranjangs(response.data))
            .catch((error) => console.log(error));
        })
        .catch((err) => console.log(err));
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs/")
      .then((response) => this.setKeranjangs(response.data))
      .catch((error) => console.log(error));
  },
  //computed untuk menjumlahkan total harga
  computed: {
    totalHarga() {
      return this.keranjangs.reduce(function (items, data) {
        return items + data.products.harga * data.jumlah_pesanan;
      }, 0);
    },
  },
};
</script>

<style>
</style>