<!-- components/ShopHeader.vue -->
<template>
    <div class="header">
        <div class="logo">🛒 我的商城</div>
        <div class="search-bar">
            <input v-model="keyword" placeholder="搜索商品..." @keyup.enter="emitSearch" />
            <button @click="emitSearch">搜索</button>
        </div>
        <div class="cart-info">
            购物车 ({{ cartCount }})
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

defineProps({
    cartCount: {
        type: Number,
        default: 0
    }
})

const emit = defineEmits(['search'])
const keyword = ref('')

function emitSearch() {
    emit('search', keyword.value)
}
</script>

<style scoped>
.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 20px;
    background: #1a3353;
    color: white;
    border-radius: 8px;
    margin-bottom: 30px;
}

.logo {
    font-size: 24px;
    font-weight: bold;
}

.search-bar input {
    padding: 8px 12px;
    border: none;
    border-radius: 4px;
    width: 250px;
    margin-right: 8px;
}

.search-bar button {
    padding: 8px 16px;
    background: #ff6600;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.cart-info {
    font-size: 16px;
}
</style>