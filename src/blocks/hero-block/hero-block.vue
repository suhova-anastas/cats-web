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
            <div class="hero__icon">
                <img src="@/images/hero-block/hero-icon.png" class="image">
            </div>
        </div>
    </div>
</template>

<script>
import Typed from 'typed.js';

export default {
    name: 'hero-block',
    mounted() {
        const optionsFirst = {
        strings: [
            'Нет подходящего мне макета для верстки?'
        ],
        typeSpeed: 40,
        startDelay: 400,
        loop: false,
        smartBackspace: true,
        showCursor: false,
        };

        const optionsSecond = {
        strings: [
            'Да ничего страшного, сделаю свой :)'
        ],
        typeSpeed: 40,
        startDelay: 3400,
        loop: false,
        smartBackspace: true,
        showCursor: false,
        };

        this.typedFirst = new Typed(this.$refs.typedFirstTitle, optionsFirst);
        this.typedSecond = new Typed(this.$refs.typedSecondTitle, optionsSecond);
    },
    beforeUnmount() {
        if (this.typedFirst) this.typedFirst.destroy();
        if (this.typedSecond) this.typedSecond.destroy();
    }
}
</script>

<style src="./hero-block.less" lang="less" />