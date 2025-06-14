<script setup>
const props = defineProps({
    error: String,
    
})
</script>

<template>
    <div v-if="props.error">{{ props.error }}</div>
</template>

<style scoped>
</style>