<template>
  <div class="home">
    <Navbar />
    <div class="container">

      <Hero />

      <div class="row mt-4">
        <div class="col-md-6">
          <h2><strong>Best </strong>Foods</h2>
        </div>
        <div class="col-md-6">
          <router-link class="btn btn-success float-right" to="/foods"> <b-icon-eye></b-icon-eye> Detail Foods</router-link>
        </div>
      </div>
      <div class="row mb-3">
        <div class="col-md-4 mt-4" v-for="product in products" :key="product.id">
        <CardProduct :product="product"/>
        </div>
      </div>
    <Footer />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Hero from '@/components/Hero.vue'
import CardProduct from '@/components/CardProduct.vue'


import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Navbar,
    Hero,
    CardProduct
    // Footer
  },
  //proses mengambil data API
  data(){
    return {
      products:[],
      search: '',
    };
  },
    methods: {
    setProducts(data){
    this.products = data;
    },
  
  },
  mounted() {
  axios
  .get('http://localhost:3000/the-best-product')
  .then((response) => this.setProducts(response.data))
  .catch((error)    => console.log(error))
  
  },
};
</script>
