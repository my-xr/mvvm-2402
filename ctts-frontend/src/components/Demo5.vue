<template>
    <!-- <li v-for="(item, index) in list">
        {{ index }} - {{ item.title }}
    </li> -->
    <!-- 对象 -->
    <li v-for="(value, key, index) in obj" :key="key">{{ index }}- {{ key }}: {{ value }}</li>
    <!-- 数字 -->
    <span v-for="n in 5" :key="n">{{ n }} </span>
</template>
<script setup>
import { ref } from 'vue'
const list = ref([{ id: 1, title: 'A' }, { id: 2, title: 'B' }])

const obj = ref({
    name: '张三',
    age: 18,
    sex: '男'
})
</script>
<style scoped>
.err {
    color: red;
    font-size: 12px;
}
</style>