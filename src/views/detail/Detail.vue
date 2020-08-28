<template>
  <div id="detail" class="wrapper">
    <DetailNavBar class="detail-nav"></DetailNavBar>
    <Scroll class="content">
      <DetailSwiper :topImages="topImages"></DetailSwiper>
      <ul>
        <li>231231</li>
        <li>10021545</li>
        <li>10021545</li>
        <li>10021545</li>
        <li>10021545</li>
        <li>10021545</li>
        <li>10021545</li>
        <li>10021545</li>
      </ul>
      <DetailBaseInfo :goods="goods"></DetailBaseInfo>
      <DetailShopInfo :shop="shop"></DetailShopInfo>
    </Scroll>
  </div>
</template>
<script>
import DetailNavBar from "./childComps/DetailNavBar";
import DetailSwiper from "./childComps/DetailSwiper";
import DetailBaseInfo from "./childComps/DetailBaseInfo";
import DetailShopInfo from "./childComps/DetailShopInfo";

import Scroll from "components/common/scroll/Scroll";

import { getDetail, Shop, Goods } from "network/detail";

export default {
  name: "Detail",
  components: {
    DetailNavBar,
    DetailSwiper,
    DetailBaseInfo,
    DetailShopInfo,
    Scroll,
  },
  data() {
    return {
      iid: null,
      topImages: [],
      goods: {},
      shop: {},
    };
  },
  created() {
    //1.保存传入的iid
    this.iid = this.$route.params.iid;

    //2.根据iid请求详情数据
    getDetail(this.iid).then((res) => {
      const data = res.result;
      //获取顶部轮播图图片
      this.topImages = data.itemInfo.topImages;

      //获取商品信息
      this.goods = new Goods(
        data.itemInfo,
        data.collumns,
        data.shopInfo.services
      );

      //创建店铺信息的对象
      this.shop = new Shop(data.shopInfo);
    });
  },
};
</script>
<style  scoped>
#detail {
  position: relative;
  height: 100vh;
  z-index: 9;
  background-color: #ffffff;
}

#detail > .detail-nav {
  position: relative;
  z-index:9;
  background-color: #ffffff;
  height: 44px;
}

#detail > .content {
  height: calc(100% - 44px);
}

</style>