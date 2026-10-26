<template>
    <div class="shop-page">
        <ShopHeader :cart-count="cartCount" @search="handleSearch" />

        <ProductList :products="filteredProducts" @add-to-cart="addToCart" />

        <ShopFooter />
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import ShopHeader from './components/ShopHeader.vue'
import ProductList from './components/ProductList.vue'
import ShopFooter from './components/ShopFooter.vue'

const searchKeyword = ref('')
const cartCount = ref(0)

const products = ref([
    { id: 1, name: '无线蓝牙耳机', price: 199, image: 'https://via.placeholder.com/200', description: '高品质音质，续航强劲', rating: 4.5, stock: 10 },
    { id: 2, name: '机械键盘', price: 399, image: 'https://via.placeholder.com/200', description: '青轴手感，办公游戏两用', rating: 4.8, stock: 5 },
    { id: 3, name: '鼠标垫大号', price: 29, image: 'https://via.placeholder.com/200', description: '加厚舒适，防水耐磨', rating: 4.2, stock: 0 },
    { id: 4, name: 'USB-C 充电线', price: 39, image: 'https://via.placeholder.com/200', description: '快充数据线，1.5米长', rating: 4.6, stock: 20 }
])

const filteredProducts = computed(() => {
    if (!searchKeyword.value) return products.value
    return products.value.filter(p =>
        p.name.includes(searchKeyword.value) ||
        p.description.includes(searchKeyword.value)
    )
})

function handleSearch(keyword) {
    searchKeyword.value = keyword
}

function addToCart(product) {
    if (product.stock > 0) {
        cartCount.value++
        product.stock--
    }
}
</script>

<style scoped>
.shop-page {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
    font-family: Arial, sans-serif;
}
</style>