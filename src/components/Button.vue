<script setup>


</script>

<template>
    <button class="button">
        <slot></slot>
    </button>
</template>

<style scoped>
    .button {
        width: 335px;
        height: 68px;
        border-radius: 100px;
        font-family: Roboto;
        font-weight: 400;
        font-size: 24px;
        line-height: 36px;
        letter-spacing: 0%;
        border: none;
        background: var(--button-bg);
        color: var(--button-color);
        display: block;
        margin: 0 auto;
    }
</style>

