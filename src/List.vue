<template>
    <VirtualList :options="props.options" />
    DOM挂载耗时：{{ time }}ms
</template>
<script setup>
import { onMounted, ref } from 'vue'
import VirtualList from './components/VirtualList.vue'

const props = defineProps({
    options: {
        type: Array,
        default: () => []
    }
})

const value = ref('')
const time = ref(0)

const t1 = Date.now()
onMounted(() => {
    const t2 = Date.now()
    time.value = t2 - t1
})
</script>
<style lang="scss" scoped></style>
