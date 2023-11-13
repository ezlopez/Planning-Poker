<template>
  <h3>{{ task.name }}</h3>
  <div class="poker-deck">
    <div v-for="card in cards" @click="castVote(card)">
      <div :class="`poker-card ${cardSelected == card ? 'selected' : ''}`">
        <p>{{ card }}</p>
      </div>
    </div>
  </div>
  <div class="button-holder">
    <button v-if="isAdmin" @click="closeVoting">Close Voting</button>
  </div>
</template>

<script setup>
// emits and props
const emit = defineEmits(["cast", "close"]);
const { task, isAdmin } = defineProps({
  task: {
    type: Object,
    required: true,
  },
  isAdmin: {
    type: Boolean,
    required: true,
  },
});

// Variables
const cards = [1, 2, 3, 5, 8, 13];
const cardSelected = ref(0);

// Functions
const castVote = (card) => {
  cardSelected.value = card;
  emit("cast", task.id, card);
};

const closeVoting = () => {
  emit("close");
};
</script>

<style scoped>
h3 {
  text-align: center;
}

button {
  font: inherit;
  padding: 0.5rem;
  background-color: rgba(112, 128, 144, 0.393);
  box-shadow: 2px 2px 2px;
  margin: 1rem;
}

.button-holder {
  display: flex;
  justify-content: flex-end;
}

.poker-deck {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 1rem;
  margin: 1rem;
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
  box-shadow: 5px 5px 5px;
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

.selected,
.selected:hover {
  background-color: slategray;
  color: aliceblue;
}

/* Spread cards out at 616px */
@media screen and (min-width: 481px) {
  .poker-deck {
    grid-template-columns: repeat(6, 1fr);
  }

  .poker-card {
    width: min(10vw, 83px);
    height: min(14.3vw, 121px);
  }

  .poker-card p {
    font-size: clamp(12px, 6vw, 50px);
  }
}
</style>
