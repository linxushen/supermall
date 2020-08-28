<template>
  <Swiper class="swiper1">
    <SwiperItem v-for="item in topImages">
        <img src="~assets/img/home/recommend_bg.jpg" alt="">
    </SwiperItem>
  </Swiper>
</template>
<script>
import {Swiper, SwiperItem} from "components/common/swiper";

export default {
  name: "DetailSwiper",
  components: {
    Swiper,
    SwiperItem,
  },
  data() {
    return {
      topImages: {
        type: Array,
        default() {
          return [];
        },
      },
    };
  },
};
</script>
<style scoped>
.swiper1 {
  height: 300px;
  overflow: hidden;
}
</style>