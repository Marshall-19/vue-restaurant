<template>
  <div class="card shadow card-product">
    <img
      :src="'assets/pict-product/' + product.gambar"
      class="card-img-top"
      alt=""
    />
    <div class="card-body">
      <h5 class="card-title">{{ product.nama }}</h5>
      <p class="card-text">Price : IDR  {{ product.harga }}</p>
      <router-link :to="'/foods/'+product.id" class="btn btn-success float-right"><b-icon-cart></b-icon-cart>Order</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ["product"],
};
</script>

<style>
</style>