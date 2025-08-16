<template>
    <div class="memecat-card">
        <img :src="data.src" class="memecat-card__image image">
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

<style src="./memecat-card.less" />