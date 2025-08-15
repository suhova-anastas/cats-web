<template>
    <div class="header">
        <div class="header__container" :class="{'header-scroll': isScroll}">
            <div class="header__logo">
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
        </div>
    </div>
</template>

<script>
import headerNavigation from '@/data/header-navigation';
import animateScrollTo from 'animated-scroll-to';

export default {
    name: 'header-block',
    data() {
        return {
            headerNavigation,
            isScroll: false,
            scrollPosition: 0,
        }
    },
    mounted() {
        window.addEventListener('scroll', this.handleScroll);
    },
    destroyed() {
        window.removeEventListener('scroll', this.handleScroll);
    },
    methods: {
        scrollTo(block, offset) {
        const element = document.querySelector(block);
            if (element) {
                animateScrollTo(element, {
                verticalOffset: offset,
                speed: 200,
                maxDuration: 200,
                minDuration: 200,
                });
            }
        },
        handleScroll() {
        this.scrollPosition = window.scrollY;
        if (this.scrollPosition > 0) {
            this.isScroll = true;
        } else if (this.scrollPosition === 0) {
            this.isScroll = false;
        }
        },
    }
}
</script>

<style src="./header-block.less" lang="less" />