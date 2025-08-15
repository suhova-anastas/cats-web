<template>
  <div class="compliment">
    <div class="compliment__container">
      <div class="compliment__title">
                <div class="compliment__title-line"></div>
                <div class="compliment__title-text">Сначала немного лучиков поддержки для вас</div>
            </div>
      <div class="compliment__swiper-container">
        <swiper v-bind="swiperConfig" class="compliment__swiper swiper" >
          <swiper-slide
            v-for="(compliment, id) in compliments"
            :key="id"
            class="compliment__swiper-slide swiper-slide"
          >
            <ComplimentCard class="compliment-card" :data="compliment"></ComplimentCard>
          </swiper-slide>
        </swiper>
        <div class="compliment__swiper-navigation">
          <div class="compliment__swiper-button-prev"></div>
          <div class="compliment__swiper-button-next"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { Swiper, SwiperSlide } from "swiper/vue";
import { Navigation } from "swiper";
import compliments from "@/data/compliments";
import ComplimentCard from "../compliment-card/compliment-card.vue";
import "swiper/css";

const swiperConfig =  {
    modules: [Navigation],
    slidesPerView: "auto",
    spaceBetween: 8,
    slideClass: "compliment__swiper-slide",
    slideActiveClass: "compliment__swiper-slide-active",
    navigation: {
      nextEl: ".compliment__swiper-button-next",
      prevEl: ".compliment__swiper-button-prev",
    },

};
</script>

<style src="./compliment-block.less" lang="less" />
