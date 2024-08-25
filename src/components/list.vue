<script setup>
import { computed, defineProps, ref } from 'vue';
const props = defineProps({
    item: {
        type: Array,
        required: true
    },
    size: {
        type: Number,
        required: true
    },
    shownumber: {
        type: Number,
        required: true
    }
})
const { item, size, shownumber } = props;
//要展示数据的起始的下标
const start = ref(0);
//要展示数据的结束的下标
const end = ref(0);
end.value = shownumber;
const containerHeight = computed(() => {
    return size * shownumber
})
//显示的数据
const showData = computed(() => {
    return item.slice(start.value, end.value)
})
//撑开的高度
const BarHeight = computed(() => {
    return size * item?.length
})
//滚动改变的top距离
const listtop = computed(() => {
    return start.value * size
})
//处理滚动事件
const handleScroll = (e) => {
    //滚动条滚动的距离
    const scrollTop = e.target.scrollTop;
    //计算出要展示数据的起始下标
    start.value = Math.floor(scrollTop / size);
    //计算出要展示数据的结束下标
    end.value = start.value + shownumber;
}
</script>
<template>
    <div class="container" :style="{ height: containerHeight + 'px' }" @scroll="handleScroll">
        <!-- 数据 -->
        <div class="list" :style="{ top: listtop + 'px' }">
            <!-- 列表 -->
            <div v-for="(item) in showData" :key="item.id" :style="{ height: size + 'px', lineHeight: size + 'px' }">{{
                item.content }}</div>
            <!-- 撑开高度 -->
            <div class="bar" :style="{ height: BarHeight + 'px' }"></div>
        </div>
    </div>
</template>
<style scoped>
.container {
    background-color: burlywood;
    overflow-y: scroll;
    font-size: 20px;
    font-weight: bold;
    width: 500px;
    margin: 0 auto;
    position: relative;
    text-align: center;
}
.list {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
}
</style>