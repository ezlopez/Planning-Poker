<template>
  <h3>{{ results.taskName }}</h3>
  <div class="outline">
    <div class="graph"></div>
    <div class="stats">
      <p>Average: {{ results.average }}</p>
      <p>Median: {{ results.median }}</p>
    </div>
    <div class="actions">
      <button class="revote-button">Re-vote</button>
      <form>
        <input type="number" required />
        <button>Set Points</button>
      </form>
    </div>
  </div>
</template>

<script setup>
// emits and props
const emit = defineEmits(["point"]);
const { results } = defineProps({
  results: {
    type: Object,
    required: true,
  },
});

// Variables
const points = ref(results.median);
</script>

<style scoped>
h3 {
  text-align: center;
}

input,
button {
  font: inherit;
  padding: 0.25rem 1rem;
}

.revote-button {
  margin: 0.5rem;
}

form {
  background-color: rgba(112, 128, 144, 0.225);
  /* border: 2px dashed rgba(0, 0, 0, 0.232); */
  padding: 0.5rem;
}

.outline {
  margin: 1rem;
}

.actions {
  display: flex;
  justify-content: flex-end;
  gap: 1.5rem;
}

.actions input {
  max-width: 2rem;
  margin-right: 0.5rem;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type="number"] {
  -moz-appearance: textfield;
}
</style>
