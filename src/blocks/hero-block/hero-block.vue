<template>
    <div class="hero">
        <div class="hero__container">
            <div class="hero__background">
                <div class="hero__background_left">
                    <img src="@/images/hero-block/hero-backround-left.svg" class="image hero__background_left-img" />
                </div>
                <div class="hero__background_right">
                    <img src="@/images/hero-block/hero-backround-right.png" class="image hero__background_right-img" />
                </div>
            </div>
            <div class="hero__content">
                <div class="hero__title_left">
                    <div class="hero__title_left-line"></div>
                    <div ref="typedFirstTitle" class="hero__title-text hero__title_left-text"></div>
                </div>
                <div class="hero__title_right">
                    <div ref="typedSecondTitle" class="hero__title-text hero__title_right-text"></div>
                    <div class="hero__title_right-line"></div>
                </div>
            </div>
            <div class="hero__icon" @click="scrollTo('.about', 0)">
                <img src="@/images/hero-block/hero-icon.png" class="image">
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import Typed from 'typed.js';
import animateScrollTo from 'animated-scroll-to';

const scrollTo = (block, offset) => {
  const element = document.querySelector(block);
  if (element) {
    animateScrollTo(element, {
      verticalOffset: offset,
      speed: 200,
      maxDuration: 200,
      minDuration: 200,
    });
  }
};

const typedFirstTitle = ref(null);
const typedSecondTitle = ref(null);

let typedFirst = null;
let typedSecond = null;

onMounted(() => {
  const optionsFirst = {
    strings: ['Нет подходящего мне макета для верстки?'],
    typeSpeed: 40,
    startDelay: 400,
    loop: false,
    smartBackspace: true,
    showCursor: false,
  };

  const optionsSecond = {
    strings: ['Да ничего страшного, сделаю свой :)'],
    typeSpeed: 40,
    startDelay: 3400,
    loop: false,
    smartBackspace: true,
    showCursor: false,
  };

  typedFirst = new Typed(typedFirstTitle.value, optionsFirst);
  typedSecond = new Typed(typedSecondTitle.value, optionsSecond);
});

onBeforeUnmount(() => {
  if (typedFirst) typedFirst.destroy();
  if (typedSecond) typedSecond.destroy();
});
</script>

<style src="./hero-block.less" lang="less" />