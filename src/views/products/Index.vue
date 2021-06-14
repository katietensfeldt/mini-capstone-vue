<template>
  <div class="products-index">
    <h1>Products</h1>
    <div class="product-card" v-for="product in products" v-bind:key="product.id">
      <h3>{{ product.name }}</h3>
      <img class="product-img" :src="product.images[0].url" alt="" />
      <h5>${{ product.price }}</h5>
    </div>
  </div>
</template>

<style scoped>
.products-index {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.product-img {
  width: 400px;
}
.product-card {
  background-color: antiquewhite;
  width: 450px;
  border-radius: 5px;
  margin: 10px;
  box-shadow: 3px 3px 3px 0.2px rgb(172, 172, 172);
  transition: all 0.2s;
}

.product-card:hover {
  box-shadow: 5px 5px 5px 0.7px rgb(172, 172, 172);
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      products: [],
    };
  },
  created: function () {
    axios
      .get("/products")
      .then((response) => {
        this.products = response.data;
        console.log(response.data);
      })
      .catch((error) => {
        console.log(error.response.errors.data);
      });
  },
};
</script>
