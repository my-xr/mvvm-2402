<template>
    <UserInfo :name="name" :age="age" @handle-click="handleClick" />
</template>
<script setup>
import UserInfo from '../components/UserInfo.vue';

import { ref } from 'vue';

const name = ref('李四');
const age = ref(22);

const handleClick = (value) => {
    console.log('接收到了值');
    name.value = value.name;
    age.value = value.age;
};

</script>
<style scoped></style>