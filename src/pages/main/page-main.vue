<template>
    <div class="page-main">
        <HeaderBlock />
        <HeroBlock />
        <AboutBlock />
        <ComplimentBlock />
    </div>
</template>

<script>
import HeaderBlock from '@/blocks/header-block/header-block.vue';
import HeroBlock from '@/blocks/hero-block/hero-block.vue';
import AboutBlock from '@/blocks/about-block/about-block.vue';
import ComplimentBlock from '@/blocks/compliment-block/compliment-block.vue';

export default {
    name: 'page-main',
    components: {
        HeaderBlock,
        HeroBlock,
        AboutBlock,
        ComplimentBlock,
    },
    data() {
        return {}
    }
}
</script>

<style />