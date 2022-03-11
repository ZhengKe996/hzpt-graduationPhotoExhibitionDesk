<template>
  <swiper
    :spaceBetween="30"
    :autoplay="{
      delay: 5000,
      disableOnInteraction: false,
    }"
    :pagination="{
      type: 'progressbar',
      clickable: true,
    }"
    :effect="'fade'"
    :navigation="true"
    :modules="modules"
    class="mySwiper"
  >
    <template v-for="item of infoMation" :key="item">
      <swiper-slide>
        <img :src="`${IMGURL}/${item.url}`" />
      </swiper-slide>
    </template>
  </swiper>
</template>

<script>
import { defineComponent } from "vue";
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from "swiper/vue";

// Import Swiper styles
import "swiper/css";

import "swiper/css/pagination";
import "swiper/css/navigation";

// import required modules
import { Autoplay, Pagination, Navigation } from "swiper";
import { IMGURL } from "@/config";

export default defineComponent({
  props: {
    infoMation: Array,
  },
  components: {
    Swiper,
    SwiperSlide,
  },
  setup() {
    return {
      modules: [Autoplay, Pagination, Navigation],
      IMGURL,
    };
  },
});
</script>

<style lang="scss" scoped>
.swiper {
  width: 65vw;
  height: 65vh;
}

.swiper-slide {
  text-align: center;
  font-size: 18px;
  background: #fff;

  /* Center slide text vertically */
  display: -webkit-box;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  -webkit-justify-content: center;
  justify-content: center;
  -webkit-box-align: center;
  -ms-flex-align: center;
  -webkit-align-items: center;
  align-items: center;

  background-position: center;
  background-size: cover;
}

.swiper-slide img {
  display: block;
  /* width: 100%; */
  height: 100%;
  object-fit: cover;
}
</style>
