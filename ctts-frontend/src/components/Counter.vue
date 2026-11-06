<template>
    <div>{{ count }}</div>
    <button @click="increment">+1</button>
</template>
<script setup>
import { ref } from 'vue'
const props = defineProps({ init: { type: Number, default: 0 } })
const emit = defineEmits(['change'])          // 声明事件
const count = ref(props.init)
const increment = () => {
    count.value++
    emit('change')                  // 触发事件，传数据
}
</script>