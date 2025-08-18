<template>
    <div class="feed">
        <div class="feed__container">
            <div class="feed__title">помогите накормить кота, пожалуйста</div>
            <div class="feed__game">
                <div v-if="!isResult" class="feed__game_variant-list">
                    <div 
                    v-for="variant in feedCat" 
                    :key="variant.id"
                    class="feed__game_variant-item"
                    :class="variant.foodVariantClass"
                    @click="handlerVariantClick(variant.id)"
                    >
                        <div class="feed__game_variant-image">
                            <img :src="variant.foodVariantImage" class="image">
                        </div>
                        <div class="feed__game_variant-text" v-html="variant.foodVariantName"></div>
                    </div>
                </div>
                <div v-if="!isResult" class="feed__game_cat-waiting">
                    <div class="feed__game_cat-waiting-image">
                        <img src="@/images/feed-block/feed-cat-reaction-waiting.png" class="image">
                    </div>
                    <div v-if="!isResult" class="feed__game_cat-waiting-bowl">
                        <img src="@/images/feed-block/feed-bowl.png" class="image">
                    </div>
                </div>
                <template v-if="isResult" v-for="reaction in feedCat">
                    <div v-if="checkCondition(reaction.condition)" class="feed__game_cat-reaction">
                        <div class="feed__game_cat-image">
                            <img :src="reaction.reactionImage" class="image">
                        </div>
                        <div
                        v-if="isResult"
                        class="feed__game_cat-reaction-text"
                        v-html="reaction.reactionText"></div>
                        <div
                        v-if="isResult"
                        class="feed__game_return-button"
                        @click="handlerReturn(reaction.condition)"
                        >вернуться назад</div>
                    </div>
                </template>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import feedCat from '@/data/feedCat';

const isResult = ref(false);
const isHolistic = ref(false);
const isFishToy = ref(false);
const isWhatThis = ref(false);
const isTreat = ref(false);
const isCucumber = ref(false);

function handlerVariantClick(id) {
    for (let item of feedCat) {
        if (item.id === id) {
            const refVar = getConditionRef(item.condition);
            refVar.value = !refVar.value
        }
    }
    isResult.value = true;
}

function checkCondition(item) {
    return getConditionRef(item).value;
}

function getConditionRef(item) {
    const mapping = {
        isHolistic,
        isFishToy,
        isWhatThis,
        isTreat,
        isCucumber
    };
    return mapping[item]
}

function handlerReturn(item) {
    isResult.value = false;
    const refVar = getConditionRef(item);
    refVar.value = !refVar.value;
}
</script>

<style src="./feed-block.less" lang="less" />