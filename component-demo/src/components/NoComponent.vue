<!-- NoComponent.vue -->
<template>
    <div class="shop-page">
        <!-- 头部 -->
        <div class="header">
            <div class="logo">🛒 我的商城</div>
            <div class="search-bar">
                <input v-model="searchKeyword" placeholder="搜索商品..." />
                <button @click="handleSearch">搜索</button>
            </div>
            <div class="cart-info">
                购物车 ({{ cartCount }})
            </div>
        </div>

        <!-- 商品列表 -->
        <div class="product-list">
            <div v-for="product in filteredProducts" :key="product.id" class="product-card">
                <img :src="product.image" :alt="product.name" class="product-image" />
                <h3 class="product-name">{{ product.name }}</h3>
                <p class="product-price">¥{{ product.price.toFixed(2) }}</p>
                <p class="product-desc">{{ product.description }}</p>
                <div class="rating">⭐ {{ product.rating }}</div>
                <button class="add-cart-btn" @click="addToCart(product)" :disabled="product.stock <= 0">
                    {{ product.stock > 0 ? '加入购物车' : '暂时缺货' }}
                </button>
            </div>
        </div>

        <!-- 底部 -->
        <div class="footer">
            <p>© 2026 我的商城 版权所有</p>
            <p>客服电话：400-888-8888</p>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 数据
const searchKeyword = ref('')
const cartCount = ref(0)
const products = ref([
    { id: 1, name: '无线蓝牙耳机', price: 199, image: 'https://via.placeholder.com/200', description: '高品质音质，续航强劲', rating: 4.5, stock: 10 },
    { id: 2, name: '机械键盘', price: 399, image: 'https://via.placeholder.com/200', description: '青轴手感，办公游戏两用', rating: 4.8, stock: 5 },
    { id: 3, name: '鼠标垫大号', price: 29, image: 'https://via.placeholder.com/200', description: '加厚舒适，防水耐磨', rating: 4.2, stock: 0 },
    { id: 4, name: 'USB-C 充电线', price: 39, image: 'https://via.placeholder.com/200', description: '快充数据线，1.5米长', rating: 4.6, stock: 20 }
])

// 计算属性
const filteredProducts = computed(() => {
    if (!searchKeyword.value) return products.value
    return products.value.filter(p =>
        p.name.includes(searchKeyword.value) ||
        p.description.includes(searchKeyword.value)
    )
})

// 方法
function handleSearch() {
    console.log('搜索:', searchKeyword.value)
}

function addToCart(product) {
    if (product.stock > 0) {
        cartCount.value++
        product.stock--
        console.log(`已将 ${product.name} 加入购物车`)
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

/* 头部样式 */
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

/* 商品列表样式 */
.product-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    gap: 20px;
    margin-bottom: 30px;
}

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

/* 底部样式 */
.footer {
    text-align: center;
    padding: 20px;
    background: #f5f5f5;
    border-radius: 8px;
    color: #666;
}
</style>