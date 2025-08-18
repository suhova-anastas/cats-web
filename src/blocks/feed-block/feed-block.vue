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
            :class="[{ dragging: draggedId === variant.id }, variant.foodVariantClass]"
            @mousedown="onPointerDown($event, variant.id)"
            @touchstart.prevent="onPointerDown($event, variant.id)"
          >
            <div class="feed__game_variant-image">
              <img :src="variant.foodVariantImage" class="image" />
            </div>
            <div
              class="feed__game_variant-text"
              v-html="variant.foodVariantName"
            ></div>
          </div>
        </div>

        <div
          v-if="!isResult"
          class="feed__game_cat-waiting"
          ref="dropzone"
        >
          <div class="feed__game_cat-waiting-image">
            <img src="@/images/feed-block/feed-cat-reaction-waiting.png" class="image" />
          </div>
          <div v-if="!isResult" class="feed__game_cat-waiting-bowl">
            <img src="@/images/feed-block/feed-bowl.png" class="image" />
          </div>
        </div>

        <template v-if="isResult" v-for="reaction in feedCat">
          <div
            v-if="checkCondition(reaction.condition)"
            class="feed__game_cat-reaction"
          >
            <div class="feed__game_cat-image">
              <img :src="reaction.reactionImage" class="image" />
            </div>
            <div
              v-if="isResult"
              class="feed__game_cat-reaction-text"
              v-html="reaction.reactionText"
            ></div>
            <div
              v-if="isResult"
              class="feed__game_return-button"
              @click="handlerReturn(reaction.condition)"
            >
              вернуться назад
            </div>
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import feedCat from "@/data/feedCat";

const isResult = ref(false);
const isHolistic = ref(false);
const isFishToy = ref(false);
const isWhatThis = ref(false);
const isTreat = ref(false);
const isCucumber = ref(false);

const draggedId = ref(null);
const dropzone = ref(null);
let dragClone = null;

function onPointerDown(e, id) {
  draggedId.value = id;
  const original = e.currentTarget;
  const rect = original.getBoundingClientRect();

  dragClone = original.cloneNode(true);
  dragClone.style.position = "fixed";
  dragClone.style.left = rect.left + "px";
  dragClone.style.top = rect.top + "px";
  dragClone.style.width = rect.width + "px";
  dragClone.style.height = rect.height + "px";
  dragClone.style.pointerEvents = "none";
  dragClone.style.zIndex = "1000";
  document.body.appendChild(dragClone);

  const moveHandler = (ev) => {
    const point = ev.touches ? ev.touches[0] : ev;
    dragClone.style.left = point.clientX - rect.width / 2 + "px";
    dragClone.style.top = point.clientY - rect.height / 2 + "px";
  };

  const upHandler = (ev) => {
    const point = ev.changedTouches ? ev.changedTouches[0] : ev;
    const dropRect = dropzone.value.getBoundingClientRect();
    const inZone =
      point.clientX >= dropRect.left &&
      point.clientX <= dropRect.right &&
      point.clientY >= dropRect.top &&
      point.clientY <= dropRect.bottom;

    if (inZone) {
        dragClone.style.transition =
            "left 0.4s ease, top 0.4s ease, transform 0.4s ease, opacity 0.4s ease";
        dragClone.style.left =
            dropRect.left + dropRect.width / 2 - rect.width / 2 + "px";
        dragClone.style.top =
            dropRect.top + dropRect.height / 2 - rect.height / 2 + "px";
        dragClone.style.transform = "scale(0.1)";
        dragClone.style.opacity = "0";

        setTimeout(() => {
            handlerVariantClick(draggedId.value);
            cleanup();
        }, 800);
    } else {
        cleanup();
    }

    document.removeEventListener("mousemove", moveHandler);
    document.removeEventListener("mouseup", upHandler);
    document.removeEventListener("touchmove", moveHandler);
    document.removeEventListener("touchend", upHandler);
  };

  document.addEventListener("mousemove", moveHandler);
  document.addEventListener("mouseup", upHandler);
  document.addEventListener("touchmove", moveHandler);
  document.addEventListener("touchend", upHandler);
}

function cleanup() {
  if (dragClone) {
    dragClone.remove();
    dragClone = null;
  }
  const originals = document.querySelectorAll(".feed__game_variant-item.dragging");
  originals.forEach((el) => el.classList.remove("dragging"));
  draggedId.value = null;
}

function handlerVariantClick(id) {
  for (let item of feedCat) {
    if (item.id === id) {
      const refVar = getConditionRef(item.condition);
      refVar.value = true;
      isResult.value = true;
    }
  }
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
    isCucumber,
  };
  return mapping[item];
}

function handlerReturn(item) {
  isResult.value = false;
  const refVar = getConditionRef(item);
  refVar.value = !refVar.value;
}
</script>

<style src="./feed-block.less" lang="less" />
