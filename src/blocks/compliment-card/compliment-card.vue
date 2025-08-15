<template>
    <div class="compliment-card">
        <img :src="data.src" class="compliment-card__image image">
    </div>
</template>

<script setup>
const props = defineProps({
    data: {
        type: Object,
        default: () => ({})
    }
})
</script>

<style src="./compliment-card.less" />