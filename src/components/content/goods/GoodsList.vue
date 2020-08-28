<template>
  <div class="goods">
    <goods-list-item v-for="item in goods" :goods-item="item" />
    <div class="test" @click="itemClick">
      <div>点击测跳转页面</div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>
  </div>
</template>

<script>
import GoodsListItem from "./GoodsListItem";

export default {
  name: "GoodsList",
  components: {
    GoodsListItem,
  },
  props: {
    goods: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  methods: {
    itemClick(){
      //console.log("跳转");
      this.$router.push('./detail/'+1111/*this.GoodsListItem.iid,应该是放在GoodListItem的*/)
    }
  }
};
</script>

<style scoped>
.goods {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;

  padding: 2px;
}
.test div{
  height: 60px;
  width: 200px;
  background-color: red;
}
</style>
