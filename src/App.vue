<template>
  <div id="app">
    <!-- 除详情页外 其他页面缓存数据 -->
    <keep-alive exclude="Detail">
      <router-view/>
    </keep-alive>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
</style>
