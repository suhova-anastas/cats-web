<template>
    <div class="recipe">
        <div class="recipe__container">
            <div class="recipe__banner">
                <div class="recipe__banner_left">
                    <div class="recipe__banner_title">подбери <span class="recipe__banner_title-orange">рецепт</span> с&nbsp;котошефом</div>
                    <div class="recipe__banner_subtitle">выбери желаемые типы блюд, а&nbsp;мы&nbsp;предложим тебе рецепты</div>
                    <div @click="$emit('popupEvent')" class="recipe__banner_button">подобрать</div>
                </div>
                <div class="recipe__banner_right">
                    <img src="@/images/recipe-block/recipe-image.png" class="recipe__banner-img image">
                </div>
            </div>
            <div class="recipe__subtitle">этот &laquo;конструктор&raquo; был взят из&nbsp;моего учебно-рабочего проекта, который, к&nbsp;сожалению, под NDA, поэтому здесь я&nbsp;добавила его изменённую версию, чтобы не&nbsp;нарушать соглашение</div>
        </div>
    </div>
</template>

<script setup>
const emit = defineEmits(['popupEvent']);
</script>

<style src="./recipe-block.less" lang="less" />