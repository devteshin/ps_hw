<script setup>
import Card from './components/Card.vue';
import Score from './components/Score.vue';
import Error from './components/Error.vue';
import { onMounted, ref, computed } from "vue";
import Button from './components/Button.vue';

const API_ENDPOINT = "http://localhost:8080/api/random-words";

function turnCard(index) {
  if (cardData.value[index].state === "closed") {
    cardData.value[index].state = "opened"
  }
  else {
    cardData.value[index].state = "closed"
  }
}

function changeStatusCard(index, newStatus) {
  cardData.value[index].status = newStatus;
  if (newStatus === "success") {
    userScore.value =  userScore.value + 10;
  }
  if (newStatus === "fail") {
    userScore.value =  userScore.value - 4;
  }
}

let userScore = ref(0);

let cardData = ref([{}]);

let error = ref();

const errorDisplay = computed(() => {
  return error.value;
});

async function getCardData() {
  try {
    const res = await fetch(`${API_ENDPOINT}`);
    if (res.status !== 200) {
      error.value = "Ошибка загрузки словаря. Статус запроса: " + res.status;
      cardData.value = null;  
      return;
    }
    error.value = null;
    cardData.value = await res.json();
    cardData.value.forEach(function (element) {
    element.state = "closed";
    element.status = "pending"
    });
  }
  catch {
    cardData.value = null;
    error.value = "Ошибка сети";
  }
};

const gameStarted = ref(false);

onMounted(()=>{
  getCardData();
});

function startGame() {
  gameStarted.value = true;
};

function resumeGame() {
  userScore.value = 0;
  getCardData();
};


</script>

<template>
  <div class="main">
    <header class="header">
        <div class="holder">
          <div>ЗАПОМНИ СЛОВО</div>
          <Score :value="userScore">
          </Score>
        </div>
    </header>
    <div  class="start-button" v-if="!gameStarted">
        <Button @click="startGame()">Начать игру</Button>
    </div>
    <div v-if="cardData && gameStarted">
      <div class="card-field">
        <Card v-for="(cardItem, index) in cardData" :key="cardItem.word"  
          @turn-card="turnCard" 
          @change-status-card="changeStatusCard" 
          v-bind="cardItem"
          :index="index"
          />
      </div>
      <div  class="resume-button">
        <Button @click="resumeGame()">Начать заново</Button>
      </div>
    </div>
    <Error  v-else :error="errorDisplay"/>
  </div>
</template>

<style scoped>
  .card-field {
    padding-left: 66px;
    padding-right: 66px;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    justify-content: space-between;
    row-gap: 1%;
    margin-bottom: 20px;
  }
  .start-button {
    flex-grow: 1;
    display: flex;  
    justify-content: center;  
    align-items: center;    
  }
</style>
