<!-- components/ProductList.vue -->
<template>
  <!-- 商品列表 -->
  <div class="product-list">
    <div
      v-for="product in filteredProducts"
      :key="product.id"
      class="product-card"
    >
      <img :src="product.image" :alt="product.name" class="product-image" />
      <h3 class="product-name">{{ product.name }}</h3>
      <p class="product-price">¥{{ product.price.toFixed(2) }}</p>
      <p class="product-desc">{{ product.description }}</p>
      <div class="rating">⭐ {{ product.rating }}</div>
      <button
        class="add-cart-btn"
        @click="addToCart(product)"
        :disabled="product.stock <= 0"
      >
        {{ product.stock > 0 ? "加入购物车" : "暂时缺货" }}
      </button>
    </div>
  </div>
</template>

<script setup>
  import { ref, computed } from "vue";

  // 数据
  const searchKeyword = ref("");
  const cartCount = ref(0);
  const products = ref([
    {
      id: 1,
      name: "无线蓝牙耳机",
      price: 199,
      image: "https://via.placeholder.com/200",
      description: "高品质音质，续航强劲",
      rating: 4.5,
      stock: 10,
    },
    {
      id: 2,
      name: "机械键盘",
      price: 399,
      image: "https://via.placeholder.com/200",
      description: "青轴手感，办公游戏两用",
      rating: 4.8,
      stock: 5,
    },
    {
      id: 3,
      name: "鼠标垫大号",
      price: 29,
      image: "https://via.placeholder.com/200",
      description: "加厚舒适，防水耐磨",
      rating: 4.2,
      stock: 0,
    },
    {
      id: 4,
      name: "USB-C 充电线",
      price: 39,
      image: "https://via.placeholder.com/200",
      description: "快充数据线，1.5米长",
      rating: 4.6,
      stock: 20,
    },
  ]);

  // 计算属性
  const filteredProducts = computed(() => {
    if (!searchKeyword.value) return products.value;
    return products.value.filter(
      (p) =>
        p.name.includes(searchKeyword.value) ||
        p.description.includes(searchKeyword.value),
    );
  });
</script>

<style scoped>
  .product-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    gap: 20px;
    margin-bottom: 30px;
  }
</style>
