<template>
  {{ props.msg }}
</template>
<script setup>

const props = defineProps({
  msg: { type: String, default: 'abc' }
})

const handleClick = () => {
}

</script>