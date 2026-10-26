<template>
    <div class="tasks">
        <h2>任务列表</h2>
        <input v-model="keyword" placeholder="搜索任务" />
        <ul>
            <li v-for="t in filteredTasks" :key="t.id">
                {{ t.title }} - {{ t.status }}
            </li>
        </ul>
        <p>已完成：{{ doneCount }} 个</p>
        <button @click="finishFirst">完成第一个</button>
        <p v-if="log">日志：{{ log }}</p>
    </div>
</template>

<script setup>
import { ref, reactive, computed, watch } from 'vue'

const keyword = ref('')
const tasks = reactive([
    { id: 1, title: '任务一：搭建项目', status: '进行中' },
    { id: 2, title: '任务二：实现登录', status: '未开始' },
    { id: 3, title: '任务三：接口联调', status: '进行中' }
])

// computed：搜索过滤
const filteredTasks = computed(() =>
    tasks.filter(t => t.title.includes(keyword.value))
)

// computed：统计已完成数量
const doneCount = computed(() => tasks.filter(t => t.status === '已完成').length)

const log = ref('')
// watch：监听任务数组变化（深度）
watch(tasks, () => {
    log.value = `任务状态变化，当前已完成 ${doneCount.value} 个`
}, { deep: true })

const finishFirst = () => {
    const t = tasks.find(x => x.status !== '已完成')
    if (t) t.status = '已完成'
}
</script>

<style scoped>
.tasks {
    max-width: 600px;
    margin: 20px auto;
    font-family: system-ui;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    padding: 10px 0;
    border-bottom: 1px solid #eee;
}

input {
    padding: 6px;
    margin-bottom: 10px;
}
</style>