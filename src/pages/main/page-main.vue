<template>
    <div class="page-main">
        <HeaderBlock />
        <HeroBlock />
        <AboutBlock />
        <ComplimentBlock />
    </div>
</template>

<script setup>
import HeaderBlock from '@/blocks/header-block/header-block.vue';
import HeroBlock from '@/blocks/hero-block/hero-block.vue';
import AboutBlock from '@/blocks/about-block/about-block.vue';
import ComplimentBlock from '@/blocks/compliment-block/compliment-block.vue';
</script>

<style src="./page-main.less" lang="less" />