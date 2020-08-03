<template>
  <div id="app">
    <router-view></router-view>
    <MainTaBar/>
  </div>
</template>

<script>
  import MainTaBar from 'components/content/mainTabbar/MainTabBar'

export default {
  name: 'App',
  components: {   
    MainTaBar
  }
}
</script>

<style>
  @import "./assets/css/base.css";
</style>
