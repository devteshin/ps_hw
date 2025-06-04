<script setup>
import ScoreIcon from './icons/ScoreIcon.vue';

const {value = 0} = defineProps({
    value: Number,
})

</script>

<template>
    <div class="score_button">
        <div class="score-value">{{ value }}</div>
        <ScoreIcon />
    </div>
</template>

<style scoped>
    .score_button {
        width: 110px;
        height: 48px;
        border-radius: 36px;
        padding: 12px 24px;
        gap: 10px;
        background: #CCE8FF;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 10px;
    }

    .score-value {
        letter-spacing: 0%;
        text-align: center;
        color: var(--button-bg);
    }

</style>


