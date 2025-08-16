<template>
  <div class="popup">
      <div class="popup__close-button" @click="$emit('popup-close')">
        <img src="/src/images/popup-block/popup-close-button.svg" class="popup__close-button-img image">
      </div>

       <div v-if="isConstructor" class="popup__constructor">
        <div class="popup__left">
          <div class="popup__left_content">
            <div class="popup__left_title">подобрать рецепт</div>
            <div class="popup__left_subtitle">выбери желаемые типы блюд, а&nbsp;мы&nbsp;предложим тебе рецепты к&nbsp;ним</div>
            <div class="popup__left_choice">
              <div
                v-for="choice in recipes"
                :key="choice.id"
                class="popup__left_choice-item"
                @click="handlerClickChoice(choice.condition)"
              >
                <div class="popup__left_choice-checkbox" :class="{ 'border-none': checkCondition(choice.condition) }">
                  <img
                    v-if="checkCondition(choice.condition)"
                    src="@/images/popup-block/popup-checkbox-true.svg"
                    class="popup__left_choice-checkbox-true">
                </div>
                <div class="popup__left_choice-text">
                  {{ choice.name }}
                </div>
            </div>
            <div
              class="popup__left_choice-item"
              @click="handlerDontKnow('iDontKnow')"
            >
              <div class="popup__left_choice-checkbox" :class="{ 'border-none': isDontKnow }">
                <img
                  v-if="isDontKnow"
                  src="@/images/popup-block/popup-checkbox-true.svg"
                  class="popup__left_choice-checkbox-true">
              </div>
              <div class="popup__left_choice-text">
                я&nbsp;не&nbsp;знаю, что хочу
              </div>
            </div>
            </div>
          </div>
          <div class="popup__left-button" @click="toggleResult()">выбрать</div>
        </div>
        <div class="popup__right">
          <div class="popup__right_background">
            <img src="/src/images/recipe-block/recipe-image.png" class="image" />
          </div>
          <div class="popup__right_zones">
            <template v-for="zone in recipes">
              <div
                class="popup__right_zone"
                :class="[zone.class, { 'zone-disabled': !checkCondition(zone.condition)}]"
              >
                <img :src="zone.image" class="image" />
              </div>
            </template>
          </div>
        </div>
       </div>

        <div v-if="isResult" class="popup__result">
          <div class="popup__result_text-content">
            <div class="popup__result_title">Твои рецепты</div>
            <div class="popup__result_subtitle">
              Подобрали рецепты по&nbsp;твоему запросу. Если ты&nbsp;хочешь вернуться и&nbsp;выбрать другие блюда, нажми кнопку &laquo;Подобрать другие&raquo;
            </div>
          </div>
          <div class="popup__result_list">
            <template v-for="item in recipes">
              <div v-if="checkCondition(item.condition)" :key="item.id" class="popup__result_item">
                <div class="popup__result_item-top">
                  <div class="popup__result_item-text">
                    <div class="popup__result_item-title">{{ item.recipeFirstName }}</div>
                    <div class="popup__result_item-subtitle">Ингредиенты:</div>
                    <div class="popup__result_item-list">
                      <div v-for="(ingredient, index) in item.recipeFirstIngredients" :key="index" class="popup__result_item-li"><div class="popup__result_item-icon"></div>{{ ingredient }}</div>
                    </div>
                  </div>
                  <img :src="item.recipeFirstImage" class="popup__result_item-image image">
                </div>
                <div class="popup__result_item-description" v-html="item.recipeFirstDescription"></div>
              </div>
              <div v-if="checkCondition(item.condition)" :key="item.id" class="popup__result_item">
                <div class="popup__result_item-top">
                  <div class="popup__result_item-text">
                    <div class="popup__result_item-title">{{ item.recipeSecondName }}</div>
                    <div class="popup__result_item-subtitle">Ингредиенты:</div>
                    <div class="popup__result_item-list">
                      <div v-for="(ingredient, index) in item.recipeSecondIngredients" :key="index" class="popup__result_item-li"><div class="popup__result_item-icon"></div>{{ ingredient }}</div>
                    </div>
                  </div>
                  <img :src="item.recipeSecondImage" class="popup__result_item-image image">
                </div>
                <div class="popup__result_item-description" v-html="item.recipeSecondDescription"></div>
              </div>
            </template>
          </div>
          <div class="popup__result_button" @click="toggleResult">Подобрать другие</div>
        </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import recipesData from '@/data/recipesData';

const emit = defineEmits(['popup-close']);

const isConstructor = ref(true);
const isResult = ref(false);
const isDessert = ref(false);
const isSoup = ref(false);
const isPaste = ref(false);
const isDrinks = ref(false);
const isMeat = ref(false);
const isChicken = ref(false);
const isFish = ref(false);
const isDontKnow = ref(false);
const arrayResult = ref([]);
const currentLink = ref('');
const recipes = ref(recipesData);

function handlerClickChoice(item) {
  const refVar = getConditionRef(item);
  refVar.value = !refVar.value;

  if (refVar.value) {
    arrayResult.value.push(item);
  } else {
    arrayResult.value.splice(arrayResult.value.indexOf(item), 1);
  }

  isDontKnow.value = false;
}

function checkCondition(item) {
  return getConditionRef(item).value;
}

function getConditionRef(item) {
  const mapping = {
    isDessert,
    isSoup,
    isPaste,
    isDrinks,
    isMeat,
    isChicken,
    isFish
  };
  return mapping[item];
}

function removeChoices() {
  arrayResult.value.forEach(choice => {
    getConditionRef(choice).value = false;
  });
  arrayResult.value = [];
}

function handlerDontKnow() {
  isDontKnow.value = !isDontKnow.value;
  removeChoices();
}

function toggleResult() {
  if (arrayResult.value.length === 0 && !isDontKnow.value) return;

  if (isDontKnow.value) {
    getRandomChoices();
  }
  isConstructor.value = !isConstructor.value;
  isResult.value = !isResult.value;

  if (!isResult.value) {
    removeChoices();
    isDontKnow.value = false;
  }
}

function getRandomChoices() {
  const arrayChoices = [];
  while (arrayChoices.length < 3) {
    const index = Math.floor(Math.random() * recipes.value.length);
    const randomCondition = recipes.value[index].condition;
    if (!arrayChoices.includes(randomCondition)) {
      arrayChoices.push(randomCondition);
      handlerClickChoice(randomCondition);
    }
  }
}
</script>

<style src="./popup-block.less" lang="less" />