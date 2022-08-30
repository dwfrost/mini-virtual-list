<template>
    <div class="visible-wrap" @scroll="onScroll">
        <div class="scroll-wrap" :style="{ height: scrollHeight + 'px' }">
            <li v-for="(item, index) of renderList" :key="index" class="li" :style="{ top: item.top + 'px' }">{{ item.label }}</li>
        </div>
    </div>
</template>
<script setup>
// @ts-nocheck

import { ref, computed } from 'vue'

const VISIBLE_HEIGHT = 170 // 可视区高度
const LI_HEIGHT = 34 // 列表项高度
const CACHE = 2 // 缓冲区

const props = defineProps({
    options: {
        type: Array,
        default: () => []
    }
})

const scrollOffset = ref(0)

const scrollHeight = computed(() => LI_HEIGHT * props.options.length)

const startIndex = computed(() => Math.floor(scrollOffset.value / LI_HEIGHT))
const endIndex = computed(() => startIndex.value + VISIBLE_HEIGHT / LI_HEIGHT)

const renderList = computed(() => {
    const options = props.options
    console.log()

    const sIndex = Math.max(0, startIndex.value - CACHE)
    const eIndex = Math.min(endIndex.value + CACHE, options.length - 1)

    const list = []
    for (let i = sIndex; i < eIndex; i++) {
        list.push({
            label: options[i].label,
            top: i * LI_HEIGHT
        })
    }
    return list
})

const onScroll = e => {
    scrollOffset.value = e.target.scrollTop
}
</script>
<style lang="scss" scoped>
.visible-wrap {
    margin: 6px 0;
    padding: 0;
    box-sizing: border-box;

    position: relative;
    overflow-y: scroll;
    // will-change: transform;
    // direction: ltr;
    height: 170px;
    width: 213px;
    .scroll-wrap {
        .li {
            list-style: none;

            font-size: var(--el-select-font-size);
            padding: 0 32px 0 20px;
            position: relative;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            color: var(--el-text-color-regular);
            height: 34px;
            line-height: 34px;
            box-sizing: border-box;
            cursor: pointer;

            position: absolute;
            left: 0px;
            // top: 0px;
            height: 34px;
            width: 100%;
        }
    }
}
</style>
