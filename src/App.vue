<script setup>
import List  from './components/list.vue';

import { ref } from 'vue'
//模拟60个数组
const list = ref(new Array(6000).fill(0).map((item, index) => {
  return {
    id: index,
    content: `name${index}`,
  }
}))
</script>

<template>
  <List :item="list" :size="60" :shownumber="10"></List>
</template>

<style scoped>

</style>
