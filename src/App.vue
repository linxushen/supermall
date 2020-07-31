<template>
  <div id="app">
    <router-view></router-view>
    <main-tab-bar/>
  </div>
</template>

<script>
  import MainTaBar from 'components/content/mainTabbar/MainabBar'

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
