<template>
    <div class="carousel-container">
      <swiper :options="swiperOptions">
        <swiper-slide v-for="n in 3" :key="n">
          <img :src="`https://via.placeholder.com/600x300?text=Slide+${n}`" alt="">
        </swiper-slide>
      </swiper>
      <div class="curvature"></div>
    </div>
  </template>
  
  <script>
  import { Swiper, SwiperSlide } from 'swiper/vue';
  import 'swiper/swiper-bundle.css';
  
  export default {
    components: {
      Swiper,
      SwiperSlide
    },
    data() {
      return {
        swiperOptions: {
          loop: true,
          slidesPerView: 1,
          spaceBetween: 30,
          pagination: {
            el: '.swiper-pagination',
            clickable: true,
          },
        }
      };
    }
  }
  </script>
  
  <style scoped>
  .carousel-container {
    position: relative;
  }
  
  .curvature {
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 50px;
    background-size: cover;
  }
  </style>
  