<template>
    <div class="notcatmeme-card">
        <img :src="data.src" class="notcatmeme-card__image image">
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

<style src="./notcatmeme-card.less" />