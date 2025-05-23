<script setup>
const props = defineProps({
	details: {
		type: Array,
		required: true,
	},
});
</script>

<template>
    <li v-for="detail in props.details">{{ detail }}</li>
</template>