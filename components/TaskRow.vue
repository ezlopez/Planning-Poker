<template>
  <tr @mouseover="isHovering = true" @mouseleave="isHovering = false">
    <td>
      <form @submit.prevent="submitEdit">
        <input
          type="text"
          v-model="editedTask.name"
          @keydown.esc="escapeEdit"
          @blur="checkBlur"
          @click="isEditing = true"
        />
      </form>
      <button v-if="isHovering && !isEditing" @click.prevent="submitVote">
        Vote
      </button>
    </td>
    <td>
      <form @submit.prevent="submitEdit">
        <input
          type="number"
          v-model="editedTask.points"
          @keydown.esc="escapeEdit"
          @blur="checkBlur"
          @click="isEditing = true"
        />
      </form>
    </td>
  </tr>
</template>

<script setup>
// emits and props
const emit = defineEmits(["edit", "vote"]);
const { task } = defineProps({
  task: {
    type: Object,
    required: true,
  },
});

// Variables
const editedTask = ref({ ...task });
const isHovering = ref(false);
const gotSubmitted = ref(false);
const isEditing = ref(false);

// Functions
const submitVote = () => {
  emit("vote", task.id);
};

const submitEdit = (event) => {
  if (JSON.stringify(editedTask) !== JSON.stringify(task)) {
    emit("edit", editedTask.value);
    gotSubmitted.value = true;
  }
  document.activeElement.blur();
};

const escapeEdit = (event) => {
  document.activeElement.blur();
};

const checkBlur = (event) => {
  if (!gotSubmitted.value) {
    editedTask.value = { ...task };
  }
  gotSubmitted.value = false;
  isEditing.value = false;
};
</script>

<style scoped>
tr {
  position: relative;
}

input {
  width: 100%;
  background-color: inherit;
  border: none;
  font: inherit;
  /* flex-grow: 1; */
}

button {
  padding: 0.25rem;
  position: absolute;
  right: 0;
  top: 0;
  height: 100%;
  /* flex-grow: 0; */
}

form {
  /* display: flex; */
  flex-flow: row nowrap;
  justify-content: space-between;
  gap: 0.5rem;
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
