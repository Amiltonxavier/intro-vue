<script setup>
import { ref } from "vue";
import Product from "./components/product.vue";
const cart = ref(0);

const premium = ref(true);
</script>

<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart{{ cart }}</div>
  <Product :premium="premium"> </Product>
</template>

