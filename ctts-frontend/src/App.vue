<template>
  <div>
    <Counter @change="handleClick" :init="count" "/>
  </div>
</template>
<script setup>
import { ref } from "vue"
import Counter from "./components/Counter.vue"

const count = ref(0)
const handleClick = () => {
}
</script>
