<template>
  <view class="navbar" :style="{ paddingTop: safeAreaInsets.top + 10 + 'px' }">
    <image class="background-image" src="@/static/search/bg_1.png" mode="aspectFill"></image>
    <view class="logo">
      <text class="logo-text"> 江苏中医在线 </text>
    </view>
    <view class="search" @click="handleSearchClick">
      <image src="@/static/search/icon_sousuo.png" />
      <text class="icon-search"> 输入关键字搜索 </text>
    </view>
  </view>
</template>
<script setup>
// 获取屏幕边界到安全区域距离
const { safeAreaInsets } = uni.getSystemInfoSync()
// 点击搜索框跳转搜索⻚⾯
const handleSearchClick = () => {
  uni.navigateTo({
    url: '/pages/search/search',
  })
}
</script>
<style lang="scss" scoped>
.navbar {
  position: relative;
  display: flex;
  flex-direction: column;
  padding-top: 20px;
  overflow: hidden; // 确保背景图不超出边界

  .background-image {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
  }

  .logo {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 64rpx;
    z-index: 1;
    padding: 0;
    .logo-text {
      line-height: 28rpx;
      color: #fff;
      font-size: 30rpx;
    }
  }

  .search {
    display: flex;
    align-items: center;
    padding: 0 20rpx;
    height: 64rpx;
    margin: 16rpx 130rpx;
    color: #bebfbc;
    font-size: 28rpx;
    border-radius: 32rpx;
    background-color: rgba(255, 255, 255);

    image {
      width: 32rpx;
      height: 32rpx;
      margin-right: 20rpx;
    }
  }
}
</style>
