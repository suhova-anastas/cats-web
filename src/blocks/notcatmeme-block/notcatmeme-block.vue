<template>
  <div class="notcatmeme">
    <div class="notcatmeme__container">
      <div class="notcatmeme__title">
                <div class="notcatmeme__title-line"></div>
                <div class="notcatmeme__title-text">Ну&nbsp;и&nbsp;напоследок ещё смешные мемчики, но&nbsp;уже не&nbsp;с&nbsp;котами :(</div>
            </div>
      <div class="notcatmeme__swiper-container">
        <swiper v-bind="swiperConfig" class="notcatmeme__swiper swiper" >
          <swiper-slide
            v-for="(notcatmeme, id) in notcatmemes"
            :key="id"
            class="notcatmeme__swiper-slide swiper-slide"
          >
            <NotcatmemeCard class="notcatmeme-card" :data="notcatmeme"></NotcatmemeCard>
          </swiper-slide>
        </swiper>
        <div class="notcatmeme__swiper-navigation">
          <div class="notcatmeme__swiper-button-prev"></div>
          <div class="notcatmeme__swiper-button-next"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { Swiper, SwiperSlide } from "swiper/vue";
import { Navigation } from "swiper";
import notcatmemes from "@/data/notcatmemes";
import NotcatmemeCard from "../notcatmeme-card/notcatmeme-card.vue";
import "swiper/css";

const swiperConfig =  {
    modules: [Navigation],
    slidesPerView: "auto",
    spaceBetween: 8,
    slideClass: "notcatmeme__swiper-slide",
    slideActiveClass: "notcatmeme__swiper-slide-active",
    navigation: {
      nextEl: ".notcatmeme__swiper-button-next",
      prevEl: ".notcatmeme__swiper-button-prev",
    },

};
</script>

<style src="./notcatmeme-block.less" lang="less" />
