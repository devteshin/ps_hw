<script setup>
import Card from './components/Card.vue';
import Score from './components/Score.vue';
import { ref } from "vue";

function turnCard() {
  console.log("turn")
}

function changeStatusCard() {
  console.log("change status")
}

let UserScore = ref(0);

let cardData = ref([
    {
      word: "car",
      translation: "автомобиль",
      state: "closed",
      status: "pending",
    },
    {
      word: "car",
      translation: "автомобиль",
      state: "opened",
      status: "pending",
    },
    {
      word: "car",
      translation: "автомобиль",
      state: "opened",
      status: "success",
    },
    {
      word: "car",
      translation: "автомобиль",
      state: "opened",
      status: "fail",
    },    
  ]
);


</script>

<template>
  <!-- <Button>Начать игру</Button> -->
  <header class="header">
      <div class="holder">
        <div>ЗАПОМНИ СЛОВО</div>
        <Score :value="UserScore">
        </Score>
      </div>
  </header>
  <Card v-for="cardItem in cardData" :key="cardItem.word" @turn-card="turnCard" @change-status-card="changeStatusCard" v-bind="cardItem"/>
</template>

<style scoped></style>
