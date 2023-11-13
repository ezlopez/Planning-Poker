<template>
  <h3>{{ task.name }}</h3>
  <div class="poker-deck">
    <div v-for="card in cards" @click="castVote(card)">
      <div :class="`poker-card ${cardSelected == card ? 'selected' : ''}`">
        <p>{{ card }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
// emits and props
const emit = defineEmits(["cast"]);
const { task } = defineProps({
  task: {
    type: Object,
    required: true,
  },
});

// Variables
const cards = [1, 2, 3, 5, 8, 13];
const cardSelected = ref(0);

// Functions
const castVote = (card) => {
  cardSelected.value = card;
  emit("cast", card);
};
</script>

<style scoped>
h3 {
  text-align: center;
}

.poker-deck {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 1rem;
  margin: 1rem auto;
  place-items: center;
}

.poker-card {
  width: 15vw;
  height: 21.5vw;
  background-color: aliceblue;
  border: 3px solid black;
  border-radius: 2vw;
  display: grid;
  place-items: center;
}

.poker-card:hover {
  background-color: rgb(111, 128, 144, 0.3);
}

.poker-card p {
  font-size: 10vw;
  margin: 0;
  padding: 0;
  user-select: none;
}

.selected {
  background-color: slategray;
}

.selected:hover {
  background-color: slategray;
}

/* Spread cards out at 616px */
@media screen and (min-width: 481px) {
  .poker-deck {
    grid-template-columns: repeat(6, 1fr);
  }

  .poker-card {
    width: 10vw;
    height: 14.3vw;
  }

  .poker-card p {
    font-size: 6vw;
  }
}
</style>
