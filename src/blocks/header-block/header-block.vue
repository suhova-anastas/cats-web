<template>
    <div class="header" :class="{ open: isOpen}">
        <div class="header__container" :class="{'header-scroll': isScroll}">
            <div class="header__logo" @click="scrollTo('.hero', 0)">
                <img src="@/images/header-block/header-logo.png" class="image" />
            </div>
            <div class="header__navigation">
                <div v-for="item in headerNavigation"
                :key="item.id"
                class="header__navigation-item"
                @click="scrollTo(item.block, item.verticalOffset, 'header__navigation-item', item.text)">
                {{ item.text }}
                </div>
            </div>
            <div class="header__burger-menu" @click="handlerOpen">
              <div class="header__burger-line" />
              <div class="header__burger-line" />
              <div class="header__burger-line" />
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import headerNavigation from '@/data/header-navigation';
import animateScrollTo from 'animated-scroll-to';

const isScroll = ref(false);
const scrollPosition = ref(0);
const isOpen = ref(false);

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

const handleScroll = () => {
  scrollPosition.value = window.scrollY;
  isScroll.value = scrollPosition.value > 0;
};

const handlerOpen = () => {
  isOpen.value = !isOpen.value;
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>
<style src="./header-block.less" lang="less" />