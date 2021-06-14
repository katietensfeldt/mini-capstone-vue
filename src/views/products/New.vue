<template>
  <div class="products-new">
    <h1>New product</h1>
    <form v-on:submit.prevent="createProduct()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="newProductParams.name" />
      <br />
      Price:
      <input type="number" v-model="newProductParams.price" />
      <br />
      Description:
      <input type="text" v-model="newProductParams.description" />
      <br />
      Inventory:
      <input type="text" v-model="newProductParams.inventory" />
      <br />
      Supplier ID:
      <input type="text" v-model="newProductParams.supplier_id" />
      <br />
      <input type="submit" value="Create" />
    </form>
    {{ newProductParams }}
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newProductParams: {},
      errors: [],
    };
  },
  methods: {
    createProduct: function () {
      axios
        .post("/products", this.newProductParams)
        .then((response) => {
          console.log("Success", response);
          this.$router.push("/products");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
