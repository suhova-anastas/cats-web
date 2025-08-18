<template>
  <div class="memecat">
    <div class="memecat__container">
      <div class="memecat__title">
                <div class="memecat__title-line"></div>
                <div class="memecat__title-text">Вы&nbsp;серьезно думали, что мы&nbsp;закончили с&nbsp;котячьими мемами?</div>
            </div>
      <div class="memecat__swiper-container">
        <swiper v-bind="swiperConfig" class="memecat__swiper swiper" >
          <swiper-slide
            v-for="(memecat, id) in memecats"
            :key="id"
            class="memecat__swiper-slide swiper-slide"
          >
            <MemecatCard class="memecat-card" :data="memecat"></MemecatCard>
          </swiper-slide>
        </swiper>
        <div class="memecat__swiper-navigation">
          <div class="memecat__swiper-button-prev"></div>
          <div class="memecat__swiper-button-next"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { Swiper, SwiperSlide } from "swiper/vue";
import { Navigation } from "swiper";
import memecats from "@/data/memecats";
import MemecatCard from "../memecat-card/memecat-card.vue";
import "swiper/css";

const swiperConfig =  {
    modules: [Navigation],
    slidesPerView: "auto",
    spaceBetween: 8,
    slideClass: "memecat__swiper-slide",
    slideActiveClass: "memecat__swiper-slide-active",
    navigation: {
      nextEl: ".memecat__swiper-button-next",
      prevEl: ".memecat__swiper-button-prev",
    },

};
</script>

<style src="./memecat-block.less" lang="less" />
