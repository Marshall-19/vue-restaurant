<template>
  <div class="hero">
    <!-- Desktop -->
    <div class="d-none d-md-block">
        <!--fungsi d-none d-md-block, untuk tampilan desktop -->
      <div class="row mt-4">
        <div class="col-md-6 mb-2">
          <div class="d-flex h-100">
            <div class="justify-centent-center align-self-center">
              <h2>
                <strong>DELICIOUS FOOD MENU </strong> <br />
                In Your Gadged
              </h2>
              <p>Lets choise your favorite foods</p>
              <!-- <button class="btn btn-success">
                Order Now
                <b-icon-arrow-right-circle-fill></b-icon-arrow-right-circle-fill>
              </button> -->
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <img src="../assets/image/hero.png" alt="" width="120%" />
        </div>
      </div>
    </div>
    <!-- mobile -->
    <div class="d-sm-block d-md-none">
        <!-- fungsi d-sm-block d-md-none, untuk tampilan mobile -->
      <div class="row mt-4">
        <div class="col-md-6 mb-2">
          <img src="../assets/image/hero.png" alt="" width="120%" />
        </div>
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-centent-center align-self-center">
              <h2>
                <strong>DELICIOUS FOOD MENU </strong> <br />
                In Your Gadged
              </h2>
              <p>Lets choise your favorite foods</p>
              <!-- <router-link class="btn btn-success" to="/foods">
                Order Now
                <b-icon-arrow-right-circle-fill></b-icon-arrow-right-circle-fill>
              </router-link> -->
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