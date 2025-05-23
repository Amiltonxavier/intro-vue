<script setup>
import { computed, ref } from "vue";
import Product from "./components/product.vue";
const cart = ref([]);

const premium = ref(true);

const updateCart = (id) => {
	cart.value.push(id);
};

const hasProductInCart = computed(() => {
	return cart.length > 0;
});

const removeFromCard = (id) => {
	if (!cart.value.includes(id)) {
		return;
	}
	const update = cart.value.filter((item) => item !== id);
	cart.value = update;
};
</script>

<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart{{ cart.length }}</div>
  <Product 
  :premium="premium" 
  @add-to-cart="updateCart" 
  @remove-from-cart="removeFromCard"
  :hasProductInCart="hasProductInCart.value"> </Product>
</template>

