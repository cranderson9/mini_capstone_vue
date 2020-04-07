<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="addProduct()">Add a new Product</button>
    <!-- <h1>{{ products }}</h1> -->
    <div v-bind:key="product.id" v-for="product in products">
      <p>name: {{ product.name }}</p>
      <p>description: {{ product.description }}</p>
      <p>price: {{ product.price }}</p>
      <!-- <p>image_url: {{ product.image_url }}</p> -->
      <img v-bind:src="product.image_url" />
      <hr />
    </div>
  </div>
</template>
<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      products: [],
    };
  },
  created: function() {
    console.log("in the created");
    console.log("this outside callback");
    axios.get("/api/products").then(response => {
      console.log("this inside callback");
      this.products = response.data;
    });
  },
  methods: {
    addProduct: function() {
      console.log("adding the Product");
      var params = {
        name: "iphone",
        description: "a cool phone",
        price: 850,
        // image_url: 'https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcSylNp-zjPToXSqmp-OEPYbaLdsF8yoh5rWW0bOtYQVVqDzYvjXQ7viCWg9lMLnbQWM7bVg0797&usqp=CAc"
      };

      axios.post("/api/products", params).then(response => {
        console.log(response.data);
        this.products.push(response.data);
      });
    },
  },
};
</script>
