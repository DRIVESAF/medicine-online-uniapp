<template>
  <view class="container">
    <!-- 横向滑动Tab栏 -->
    <scroll-view class="tab-bar" scroll-x :scroll-left="scrollLeft">
      <view
        v-for="(tab, index) in tabList"
        :key="index"
        class="tab-item"
        :class="{ active: currentTab === index }"
        @click="changeTab(index)"
      >
        {{ tab.name }}
      </view>
    </scroll-view>

    <!-- Tab 对应内容区域 -->
    <view
      class="tab-content"
      @touchstart="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
    >
      <view v-if="currentTab === 0">
        <ShangXin />
      </view>
      <view v-else-if="currentTab === 1">
        <ZiXun />
      </view>
      <view v-else-if="currentTab === 2">
        <XueXi />
      </view>
      <view v-else-if="currentTab === 3">
        <ZhiShiKu />
      </view>
      <view v-else-if="currentTab === 4">
        <KaoHe />
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref, nextTick } from 'vue'

// 子组件导入
import ShangXin from './TabContent/ShangXin.vue'
import ZiXun from './TabContent/ZiXun.vue'
import XueXi from './TabContent/XueXi.vue'
import ZhiShiKu from './TabContent/ZhiShiKu.vue'
import KaoHe from './TabContent/KaoHe.vue'

// 定义 Tab 列表
const tabList = [
  { name: '上新资源' },
  { name: '资讯' },
  { name: '学习' },
  { name: '知识库' },
  { name: '考核' },
]

// 当前激活的 Tab
const currentTab = ref(0)

// ScrollView 滚动位置
const scrollLeft = ref(0)

// 切换 Tab
const changeTab = (index) => {
  currentTab.value = index
  scrollToCurrentTab()
}

// 滚动到当前 Tab
const scrollToCurrentTab = () => {
  nextTick(() => {
    const tabItemWidth = 200 // 假设每个 Tab 的宽度为 200rpx（需要根据实际情况调整）
    const containerWidth = uni.getSystemInfoSync().screenWidth
    const targetPosition = currentTab.value * tabItemWidth
    const offset = targetPosition - (containerWidth / 2 - tabItemWidth / 2)
    scrollLeft.value = offset < 0 ? 0 : offset
  })
}

// 触摸滑动切换功能
let startX = 0
let endX = 0

const handleTouchStart = (e) => {
  startX = e.changedTouches[0].pageX
}

const handleTouchMove = (e) => {
  endX = e.changedTouches[0].pageX
}

const handleTouchEnd = () => {
  const deltaX = endX - startX
  if (Math.abs(deltaX) > 50) {
    if (deltaX < 0 && currentTab.value < tabList.length - 1) {
      // 向左滑动，切换到下一个 tab
      currentTab.value += 1
      scrollToCurrentTab()
    } else if (deltaX > 0 && currentTab.value > 0) {
      // 向右滑动，切换到上一个 tab
      currentTab.value -= 1
      scrollToCurrentTab()
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  height: auto;
}

.tab-bar {
  display: flex;
  white-space: nowrap;
  padding: 10rpx 0;
  border-bottom: 1rpx solid #e9e9e9;

  .tab-item {
    display: inline-block;
    width: 200rpx; /* 假设每个 Tab 宽度为 200rpx */
    text-align: center;
    padding: 20rpx 0;
    margin: 0 30rpx;
    font-size: 30rpx;
    color: #666;
    position: relative;
  }

  .tab-item.active {
    color: #029d57;
  }

  .tab-item.active::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 50%;
    width: 50rpx;
    height: 4rpx;
    background-color: #029d57;
    transform: translateX(-50%);
    border-radius: 2rpx;
  }
}

.tab-content {
  flex-grow: 1;
  overflow-y: auto;
  padding: 20rpx;
  box-sizing: border-box;
}
</style>
