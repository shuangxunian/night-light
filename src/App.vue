<script setup lang="ts">
import { ref } from 'vue'
interface ItemWithColor {
  id: number;
  name: string;
  status: boolean;
  color: string;
}

const selectLight  = ref<ItemWithColor>()

const lightList = ref([
  { id: 1, name: '灯1', status: false, color: '#5c657f' },
  { id: 2, name: '灯2', status: false, color: '#5e84a5' },
  { id: 3, name: '灯3', status: false, color: '#5ea594' },
  { id: 4, name: '灯4', status: false, color: '#5e6aa5' },
  { id: 5, name: '灯5', status: false, color: '#aaa' },
  { id: 6, name: '灯6', status: false, color: '#ccc' },
  { id: 7, name: '灯7', status: false, color: '#fff' },
])

const openLight = (item: ItemWithColor) => {
  selectLight.value = item
}

const offLight = () => {
  selectLight.value = undefined
}

// 保持屏幕常亮
navigator.wakeLock.request('screen').then(function () {
  console.log('屏幕常亮已开启');
}).catch(function (error) {
  console.log('屏幕常亮错误：', error);
});

</script>

<template>
  <div v-if="selectLight" class="main" :style="{ backgroundColor: selectLight.color }" @click="offLight"></div>
  <div v-else class="main">
    <div class="light-list">
      <div class="light" v-for="item in lightList" :key="item.id" :style="{ backgroundColor: item.color }" @click="openLight(item)"></div>
    </div>
  </div>
</template>

<style scoped>
.main {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #eee;
}

.light-list {
  width: 100%;
  height: 100px;
  background-color: #fff;
  display: flex;
  gap: 8px;
}

.light {
  flex: 1;
}


</style>
