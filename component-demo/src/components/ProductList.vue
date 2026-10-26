<!-- components/ProductList.vue -->
<template>
    <div class="product-list">
        <ProductCard v-for="product in products" :key="product.id" :product="product"
            @add-to-cart="$emit('add-to-cart', product)" />
    </div>
</template>

<script setup>
import ProductCard from './ProductCard.vue'

defineProps({
    products: {
        type: Array,
        required: true
    }
})

defineEmits(['add-to-cart'])
</script>

<style scoped>
.product-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    gap: 20px;
    margin-bottom: 30px;
}
</style>