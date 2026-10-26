<!-- components/ProductCard.vue -->
<template>
    <div class="product-card">
        <img :src="product.image" :alt="product.name" class="product-image" />
        <h3 class="product-name">{{ product.name }}</h3>
        <p class="product-price">¥{{ product.price.toFixed(2) }}</p>
        <p class="product-desc">{{ product.description }}</p>
        <div class="rating">⭐ {{ product.rating }}</div>
        <button class="add-cart-btn" @click="$emit('add-to-cart')" :disabled="product.stock <= 0">
            {{ product.stock > 0 ? '加入购物车' : '暂时缺货' }}
        </button>
    </div>
</template>

<script setup>
defineProps({
    product: {
        type: Object,
        required: true
    }
})

defineEmits(['add-to-cart'])
</script>

<style scoped>
.product-card {
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    padding: 15px;
    transition: box-shadow 0.3s;
}

.product-card:hover {
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.product-image {
    width: 100%;
    height: 180px;
    object-fit: cover;
    border-radius: 4px;
    margin-bottom: 10px;
}

.product-name {
    font-size: 18px;
    margin: 8px 0;
    color: #333;
}

.product-price {
    font-size: 22px;
    color: #ff4400;
    font-weight: bold;
    margin: 8px 0;
}

.product-desc {
    color: #666;
    font-size: 14px;
    margin: 8px 0;
}

.rating {
    color: #f39c12;
    margin: 8px 0;
}

.add-cart-btn {
    width: 100%;
    padding: 10px;
    background: #1a3353;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
}

.add-cart-btn:disabled {
    background: #ccc;
    cursor: not-allowed;
}
</style>