<script setup>
import Card from './components/Card.vue';
import Score from './components/Score.vue';

function turnCard() {
  console.log("turn")
}

function changeStatusCard() {
  console.log("change status")
}

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
  <Card @turn-card="turnCard" @change-status-card="changeStatusCard"/>


</template>

<style scoped></style>
