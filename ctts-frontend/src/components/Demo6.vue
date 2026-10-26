<template>
    <div class="app">
        <LoginForm :init-name="defaultName" @submit="onLogin" />
        <p v-if="msg">{{ msg }}</p>
    </div>
</template>
<script setup>
import { ref } from 'vue'
import LoginForm from './LoginForm.vue'
const defaultName = ref('admin')
const msg = ref('')
const onLogin = (data) => {                                  // 接收子组件数据
    msg.value = `登录：${data.username} / ${data.password}`
}
</script>
<style scoped></style>