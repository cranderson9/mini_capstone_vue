<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>
      Name:
      <input type="text" v-model="newProductName" />
    </p>
    <p>
      Description:
      <input type="text" v-model="newProductDescription" />
    </p>
    <p>
      Price:
      <input type="text" v-model="newProductPrice" />
    </p>
    <p>
      Image_url:
      <input type="text" v-model="newProductImage_url" />
    </p>
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
      newProductName: "",
      newProductDescription: "",
      newProductPrice: "",
      newProductImage_url: "",
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
      console.log(this.newProductName);
      var params = {
        name: this.newProductName,
        description: this.newProductDescription,
        price: this.newProductPrice,
        image_url: this.newProductImage_url,
      };

      axios.post("/api/products", params).then(response => {
        console.log(response.data);
        this.products.push(response.data);
        this.newProductName;
        this.newProductDescription;
        this.newProductPrice;
        this.newProductImage_url;
      });
    },
  },
};
</script>
