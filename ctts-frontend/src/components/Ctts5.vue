<template>
    <!-- 点击链接会跳转 -->
    <a href="https://baidu.com" @click="handleLink">去百度</a>

    <!-- 提交表单会刷新页面 -->
    <form @submit="handleSubmit">
        <button type="submit">提交</button>
    </form>
</template>

<script setup>
function handleLink() {
    console.log('父级被点了')
}
function handleSubmit() {
    console.log('子级被点了')
}
</script>