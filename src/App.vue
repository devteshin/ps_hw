<script setup>
import Card from './components/Card.vue';
import Score from './components/Score.vue';
import Error from './components/Error.vue';
import { onMounted, ref, computed } from "vue";

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
  cardData.value[index].status = newStatus
}

let UserScore = ref(0);

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
  <div class="card-field" v-if="cardData">
    <Card v-for="(cardItem, index) in cardData" :key="cardItem.word"  
      @turn-card="turnCard" 
      @change-status-card="changeStatusCard" 
      v-bind="cardItem"
      :index="index"
      />
  </div>
  <Error  v-else :error="errorDisplay"/>
</template>

<style scoped>
  .card-field {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    row-gap: 1%;
  }
</style>
