<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newProductParams: {},
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createProduct() {
      axios
        .post("/products", this.newProductParams)
        .then((response) => {
          console.log("products.create", response);
          this.$router.push("products");
        })
        .catch((error) => {
          console.log("products create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
<template>
  <div class="products-new">
    <h1>New product</h1>
    <form v-on:submit.prevent="createProduct()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="newProductParams.name" />
      Price:
      <input type="text" v-model="newProductParams.price" />
      Description:
      <input type="text" v-model="newProductParams.description" />
      <input type="submit" value="Create" />
    </form>
  </div>
</template>

<style></style>
