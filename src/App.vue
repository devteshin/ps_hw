<script setup>
  const now = new Date();
  const shortDate = new Intl.DateTimeFormat("ru", {dateStyle: "short"}).format(now);
</script>

<template>
  <main>{{ shortDate }}</main>
</template>

<style scoped></style>
