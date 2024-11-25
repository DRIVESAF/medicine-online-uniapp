<template>
  <view class="index">
    <CustomNavbar />
    <ScrollView />
  </view>
</template>
<script setup>
import CustomNavbar from './components/CustomNavbar.vue'
import ScrollView from './components/ScrollView.vue'
</script>
<style lang="scss" scoped>
page {
  background-color: #f7f7f7;
  height: 100%;
  overflow: hidden;
}
.index {
  height: 100%;
  display: flex;
  flex-direction: column;
}
</style>
