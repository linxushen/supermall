<template>
  <div id="home" class="wrapper">
    <NavBar class="home-nav">
      <div slot="center">购物街</div>
    </NavBar>
    <TabControl 
        :titles="['流行','新款','精选']" 
        @tabClick="tabClick"
        ref="tabControl1" class="tab-control" v-show="isTabFixed"></TabControl>
    <Scroll class="content" ref="scroll" 
    :probe-type="3" 
    @scroll="contentScroll" 
    :pull-up-load="true" @pullingUp="loadMore">
      <HomeSwiper :banners="banners" @swiperImageLoad="swiperImageLoad"></HomeSwiper>
      <RecommendView :recommends="recommends"></RecommendView>
      <FeatureView></FeatureView>
      <TabControl 
        :titles="['流行','新款','精选']" 
        @tabClick="tabClick"
        ref="tabControl2"></TabControl>
      <GoodsList :goods="showGoods"></GoodsList>
    </Scroll>
    <BackTop @click.native="backClick" v-show="isShowBackTop"></BackTop>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import HomeSwiper from "./childComps/HomeSwiper";
import RecommendView from "./childComps/RecommendView";
import FeatureView from "./childComps/FeatureView";

import TabControl from "components/content/tabControl/TabControl";
import GoodsList from "components/content/goods/GoodsList";
import Scroll from "components/common/scroll/Scroll";
import BackTop from "components/content/backTop/BackTop";

import { getHomeMultidata, getHomeGoods } from "network/home";

export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TabControl,
    GoodsList,
    Scroll,
    BackTop,
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] },
      },
      currentType: "pop",
      isShowBackTop:false,
      tabOffsetTop: 0,
      isTabFixed:false,
      saveY:0
    };
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list;
    },
  },
  activated () {
    this.$refs.scroll.scrollTo(0,this.saveY,0)
    this.$refs.scroll.scroll.refresh()
  },
  deactivated () {
    // console.log(this.$refs.scroll.getScrollY());
    this.saveY =this.$refs.scroll.getScrollY();
  },
  created() {
    console.log("home create");
    //1.请求多个数据
    this.getHomeMultidata();

    //2.请求商品数据
    // this.getHomeGoods('pop');
    // this.getHomeGoods('new');
    // this.getHomeGoods('sell');

  },
  mounted () {
    
  },
  methods: {
    /*
      事件监听
    */
    tabClick(index) {
      switch (index) {
        case 0:
          this.currentType = "pop";
          break;
        case 1:
          this.currentType = "new";
        case 2:
          this.currentType = "sell";
      }
      this.$refs.tabControl1.currentIndex = index;
      this.$refs.tabControl2.currentIndex = index;
    },
    backClick() {
      //回到顶部
      this.$refs.scroll.scrollTo(0, 0, 500);
      // console.log(scroll);
    },
    contentScroll(position){
      //console.log(position);
      //判断BackTop是否显示
      this.isShowBackTop = (-position.y) > 1000
      
      //决定tabControll是否吸顶（position：fixed）
      this.isTabFixed = (-position.y) > this.tabOffsetTop
    },
    loadMore(){
      //console.log("加载更多");
      this.getHomeGoods(this.currentType)

      this.$refs.scroll.scroll.refresh()
    },
    swiperImageLoad(){
      this.tabOffsetTop = this.$refs.tabControl2.$el.offsetTop;
      //console.log(this.$refs.tabControl2.$el.offsetTop);
    },
    /*
      网络请求
    */
    getHomeMultidata() {
      getHomeMultidata().then((res) => {
        //console.log(res);
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then((res) => {
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1;
        // console.log(res)

        this.$refs.scroll.finishPullUp()
      });
    },
  },
};
</script>

<style scoped>
#home {
  height: 100vh;
  position: relative;
}

.home-nav {
  background-color: var(--color-tint);
  color: white;
  /* position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9; */
}
/* .tab-control {
  position: sticky;
  top: 44px;
} */
.content {
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
}

.tab-control{
  position: relative;
  z-index: 9;
}


</style>
