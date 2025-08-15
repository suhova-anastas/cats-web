<template>
    <div class="compliment-card">
        <img :src="data.src" class="compliment-card__image image">
    </div>
</template>

<script>
export default {
    name: 'compliment-card',
    props: {
        data: {
            type: Object,
            default: () => ({})
        },
    },
}
</script>

<style src="./compliment-card.less" />