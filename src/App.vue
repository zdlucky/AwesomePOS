<template>
  <div id="app">
    <leftNav/>
    <router-view/>
  </div>
</template>

<script>
import leftNav from '@/components/common/leftNav';

export default {
  name: 'App',
  components: {
    leftNav
  }
}
</script>

<style>
/* 引入重置样式，此处引用跟在 main.js 引用效果一样 */
/* @import './assets/reset.css'; */
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
