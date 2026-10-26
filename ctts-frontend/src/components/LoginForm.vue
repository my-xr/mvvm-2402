<template>
    <form @submit.prevent="onSubmit">
        <input v-model.trim="form.username" placeholder="用户名" />
        <input v-model.trim="form.password" type="password" placeholder="密码" />
        <button type="submit">登录</button>
    </form>
</template>
<script setup>
import { reactive } from 'vue'
defineProps({ initName: { type: String, default: '' } })   // 父传初始用户名
const emit = defineEmits(['submit'])                        // 声明事件
const form = reactive({ username: '', password: '' })
const onSubmit = () => {
    emit('submit', { username: form.username, password: form.password })  // 子传父
}
</script>