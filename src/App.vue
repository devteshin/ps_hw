<script setup>
import Card from './components/Card.vue';
import Score from './components/Score.vue';
import { onMounted, ref } from "vue";

const API_ENDPOINT = "http://localhost:8080/api/random-words";

function turnCard() {
  console.log("turn")
}

function changeStatusCard() {
  console.log("change status")
}

let UserScore = ref(0);

let cardData = ref([{}]);

let error = ref();

async function getCardData() {
  const res = await fetch(`${API_ENDPOINT}`);
  if (res.status !== 200) {
    error.value = await res.json();
    cardData.value = null;  
    return;
  }
  error.value = null;
  cardData.value = await res.json();
  cardData.value.forEach(function (element) {
  element.state = "closed";
  element.status = "pending"
  });
};

onMounted(()=>{
  getCardData();
});

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
  <div class="card-field">
    <Card v-for="cardItem in cardData" :key="cardItem.word"  
      @turn-card="turnCard" 
      @change-status-card="changeStatusCard" 
      v-bind="cardItem"/>
  </div>
</template>

<style scoped>
  .card-field {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    row-gap: 1%;
  }
</style>
