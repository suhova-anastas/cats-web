<template>
    <div class="compliment">
        <div class="compliment__container">
            <div class="compliment__title">
                <div class="compliment__title-line"></div>
                <div class="compliment__title-text">Сначала немного лучиков поддержки для вас</div>
            </div>
            <div class="compliment__swiper-container">
                <swiper class="compliment__swiper swiper" :options="swiperOptions">
                    <swiper-slide
                        v-for="(compliment, id) in compliments"
                        :key="id"
                        class="compliment__swiper-slide swiper-slide"
                    >
                        <compliment-card class="compliment-card" :data="compliment"></compliment-card>
                    </swiper-slide>
                </swiper>
            </div>
        </div>
    </div>
</template>

<script>
import { Swiper, SwiperSlide } from 'vue-awesome-swiper';
import compliments from '@/data/compliments';
import ComplimentCard from '../compliment-card/compliment-card.vue';
import 'swiper/css';

export default {
    name: 'copliment-block',
    components: {
        ComplimentCard,
        Swiper,
        SwiperSlide
    },
    data() {
        return {
            compliments,
        }
    },
    computed: {
        swiperOptions() {
            return {
                slidesPerView: 'auto',
                spaceBetween: 8,
                loop: true,
                centeredSlides: true,
                wrapperClass: 'compliment__swiper-wrapper',
                slideClass: 'compliment__swiper-slide',
                slideActiveClass: 'compliment__swiper-slide-active',
                navigation: {
                nextEl: '.compliment__swiper-button-next',
                prevEl: '.compliment__swiper-button-prev',
                },
                breakpoints: {
                1023: {
                    spaceBetween: 20,
                    loop: false,
                    centeredSlides: false,
                },
                },
            };
        },
    },
}
</script>

<style src="./compliment-block.less" lang="less" />