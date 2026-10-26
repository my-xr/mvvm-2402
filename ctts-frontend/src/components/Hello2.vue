<template>
    <div class="home">
        <header class="header">
            <h1>CTTS-Frontend</h1>
            <p>校园实训任务管理系统</p>
        </header>

        <main class="main">
            <h2>实训项目列表</h2>
            <ul class="project-list">
                <li v-for="project in filteredProjects" :key="project.id" class="project-item">
                    <span class="title">{{ project.title }}</span>
                    <span class="status">{{ project.status }}</span>
                </li>
            </ul>

            <div class="counter">
                <p>本页访问次数：{{ visitCount }}</p>
                <button @click="visitCount++">增加访问</button>
                <button @click="resetCount">重置</button>
            </div>
            <h2>搜索</h2>
            <input v-model="text" placeholder="输入" /> {{ text }}
            <button @click.stop="handleSearch">搜索</button>
            <button @click.prevent="resetSearch">重置</button>

            <h2>列表</h2>

        </main>
    </div>
</template>

<script setup>

import { ref, reactive, computed, shallowRef } from 'vue'

const visitCount = ref(0)
const resetCount = () => {
    visitCount.value = 0
}

// 过滤项目
const projects = shallowRef([
    { id: 1, title: "Java", status: "进行中" },
    { id: 2, title: "Vue", status: "已完成" }
])

// handleClick
const handleClick = () => {
    console.log("button")
}

// 是否可用 
const isDisabled = ref(true)

//  搜索文本
const text = ref("Java")

// 处理搜索
const handleSearch = () => {
    projects.value.filter(o => o.title.includes(text.value))
}

// 过滤项目
const filteredProjects = computed(() => {
    if (!text.value) return projects.value
    return projects.value.filter(o => o.title.includes(text.value))
})

// 总访问次数
const total = computed(() => visitCount.value)

// 重置搜索
const resetSearch = () => {
    text.value = ""
    score.value = 50
    isVisible.value = false
}

// 分数
const score = ref(70)

const isVisible = ref(true)

const list = ref([
    { id: 1, title: '项目一' },
    { id: 2, title: '项目二' }
])

</script>
<style lang="css" scoped>
.home {
    max-width: 800px;
    margin: 0 auto;
    font-family: system-ui, sans-serif;
    color: #333;
}

.header {
    text-align: center;
    padding: 30px 0;
    border-bottom: 2px solid #42b883;
}

.header h1 {
    color: #42b883;
    margin: 0;
}


.project-list {
    list-style: none;
    padding: 0;
}

.project-item {
    display: flex;
    justify-content: space-between;
    padding: 12px 0;
    border-bottom: 1px solid #eee;
}

.project-item .status {
    color: #999;
    font-size: 14px;
}

.counter {
    margin-top: 30px;
    text-align: center;
}

button {
    padding: 6px 16px;
    margin: 0 6px;
    border: 1px solid #42b883;
    background: #fff;
    color: #42b883;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background: #42b883;
    color: #fff;
}
</style>