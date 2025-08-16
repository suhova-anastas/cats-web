<template>
    <div class="page-main">
        <PopupBlock v-if="isPopup" @popupClose="closePopup" />
        <HeaderBlock />
        <HeroBlock />
        <AboutBlock />
        <ComplimentBlock />
        <RecipeBlock @popupEvent="openPopup" />
    </div>
</template>

<script setup>
import { ref } from 'vue';
import PopupBlock from '@/blocks/popup-block/popup-block.vue';
import HeaderBlock from '@/blocks/header-block/header-block.vue';
import HeroBlock from '@/blocks/hero-block/hero-block.vue';
import AboutBlock from '@/blocks/about-block/about-block.vue';
import ComplimentBlock from '@/blocks/compliment-block/compliment-block.vue';
import RecipeBlock from '@/blocks/recipe-block/recipe-block.vue';

const isPopup = ref(false);

function openPopup() {
    isPopup.value = true;
    document.body.classList.add('overflow-hidden');
}

function closePopup() {
    isPopup.value = false;
    document.body.classList.remove('overflow-hidden');
}
</script>

<style src="./page-main.less" lang="less" />
