<template>
    <div class="play-container">
        <div class="item">
            数据量：
            <el-select v-model="total" @change="onChange">
                <el-option v-for="item in totalOptions" :key="item" :label="item" :value="item" />
            </el-select>
            条
        </div>
        <template v-if="show">
            <div class="item">
                <List :options="options" />
            </div>
        </template>
    </div>
</template>

<script setup>
import { computed, nextTick, ref } from 'vue'
import List from './List.vue'

const initials = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']

const total = ref(10000)
const totalOptions = [10, 100, 1000, 10000, 50000]
const onChange = () => {
    show.value = false
    nextTick(() => {
        show.value = true
    })
}

const show = ref(true)
const options = computed(() => {
    return Array.from({ length: total.value }).map((_, idx) => ({
        value: `Option ${idx + 1}`,
        label: `${initials[idx % 10]}${idx}`
    }))
})
</script>

<style lang="scss">
html,
body {
    width: 100vw;
    height: 100vh;
    margin: 0;

    .play-container {
        height: 100%;
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;

        .item {
            margin: 10px 0;
        }
    }
}
</style>
