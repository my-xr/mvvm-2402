<template>
    <div>
        姓名：{{ props.name }}
        年龄：{{ props.age }}
    </div>
    <button @click="handleClick">
        修改用户信息
    </button>
</template>
<script setup>
const props = defineProps({
    name: { type: String, required: true },
    age: { type: Number, required: true }
})

const emits = defineEmits(['handle-click'])

const handleClick = () => {

    emits('handle-click', { name: '刘6', age: 66 })
}
</script>
<style scoped></style>