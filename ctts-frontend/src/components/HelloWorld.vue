<template>
  <div :style="{ color: textColor, fontSize: size + 'px' }">你好</div>

  {{ size }}
</template>


<script setup>
import { ref } from 'vue'

const textColor = ref('blue')  // {value: blue}
const size = ref(24)

textColor.value = 'red'
size.value = 48


</script>

<style scoped></style>