<script setup>
import Card from './components/Card.vue';
import Score from './components/Score.vue';
</script>

<template>
  <!-- <Button>Начать игру</Button> -->
  <header class="header">
      <div class="holder">
        <div>ЗАПОМНИ СЛОВО</div>
        <Score :value="100">
          
        </Score>
      </div>
  </header>
  <Card />


</template>

<style scoped></style>
