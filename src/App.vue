<template>
  <div id="app">
    <!-- 将Detail.vue排除在keep-alive之外 -->
    <keep-alive exclude="Detail">
      <router-view></router-view>
    </keep-alive>
    <MainTaBar />
  </div>
</template>

<script>
import MainTaBar from "components/content/mainTabbar/MainTabBar";

export default {
  name: "App",
  components: {
    MainTaBar,
  },
};
</script>

<style>
@import "./assets/css/base.css";
</style>
