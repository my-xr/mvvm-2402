<template>
    <!-- <p>{{ count }}</p> <!-- 模板自动解包 -->
    <!-- <button @click="count++">+1</button>

    <p>{{ state.name }}</p>
    <p>{{ state.age }}</p>
    <button @click="handleAge">年龄+1</button>
    <button @click="handleState">整体替换</button> -->
    <p>{{ state.name }}</p>
    <button @click="handleState">改名字</button>

    <p>单价：{{ price }}</p>
    <p>数量：{{ count }}</p>
    <p>总价：{{ total }}</p>
    <button @click="count++">数量+1</button>
    <button @click="price++">单价+1</button>

    <p v-if="isShow">count+1了</p>
</template>
<script setup>

import { reactive, ref, computed, watch, watchEffect } from 'vue'

// const count = ref(0)

const state = reactive({ name: '张三', age: 18 })

// const handleAge = () => {
//     state.age++
// }

const handleState = () => {
    state.name = '王五'
}
const price = ref(50)
const count = ref(2)

const total = computed(() => {
    return price.value * count.value
})

const isShow = ref(false)

watch([count, () => state.name], ([newCount, newTotal], [oldCount, oldTotal]) => {
    console.log(newCount, newTotal)
    console.log(oldCount, oldTotal)
})


watchEffect(() => {
    console.log(total.value)
})

</script>