<script setup lang="ts">
import { ref, computed, type ComputedRef } from "vue";
import socksGreenImage from "../assets/images/socks_green.jpeg";
import socksBlueImage from "../assets/images/socks_blue.jpeg";
import ProductDetails from "./productDetails.vue";

const props = defineProps<{
	premium: boolean;
	hasProductInCart: ComputedRef<boolean>;
}>();

const emit = defineEmits(["add-to-cart", "remove-from-cart"]);

const product = ref("Socks");

const details = ref(["50% cotton", "30% wool", "20% polyester"]);
const shipping = computed(() => {
	if (props.premium) {
		return "Free";
	}

	return 2.99;
});
const selectedVariant = ref(0);
const brand = ref("Vue Mastery");

const variants = ref([
	{
		id: 2234,
		color: "green",
		image: socksGreenImage,
		quantity: 50,
		onSale: true,
	},
	{
		id: 2235,
		color: "blue",
		image: socksBlueImage,
		quantity: 10,
		onSale: false,
	},
]);

const image = computed(() => {
	return variants.value[selectedVariant.value].image;
});

const title = computed(() => {
	return `${brand.value} ${product.value} ${onSale.value ? "- On Sale" : ""}`;
});

const inStock = computed(() => {
	return variants.value[selectedVariant.value].quantity > 0;
});

const onSale = computed(() => {
	return variants.value[selectedVariant.value].onSale;
});

const addToCard = () => {
	emit("add-to-cart", variants.value[selectedVariant.value].id);
};

const removeFromCard = () => {
	emit("remove-from-cart", variants.value[selectedVariant.value].id);
};

const updateVariant = (index) => {
	selectedVariant.value = index;
};
</script>

<template>
      <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img :src="image">
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock">In Stock</p>
          <p v-else>Out of Stock</p>
        <p>Shipping: {{ shipping }}</p>
          <ul>
            <ProductDetails :details="details"></ProductDetails>
          </ul>

          <div v-for="(variant, index) in variants" 
          :key="variant.id" 
          class="color-circle"
          @mouseover="updateVariant(index)"
          :style="{ backgroundColor: variant.color}"
          >
          </div>
          <button :disabled="!inStock" 
          class="button" 
          :class="{disabledButton: !inStock}" 
          v-on:click="addToCard">Add to Card</button>
          <button  class="button" v-if="hasProductInCart" @click="removeFromCard">
            Remove 
        </button>
      </div>
    </div>
  </div>
</template>