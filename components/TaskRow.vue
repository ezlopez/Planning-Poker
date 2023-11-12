<template>
  <tr>
    <td>
      <form @submit.prevent="submitEdit">
        <input
          type="text"
          v-model="editedTask.name"
          @keydown.esc="escapeEdit"
        />
      </form>
    </td>
    <td>
      <form @submit.prevent="submitEdit">
        <input
          type="number"
          v-model="editedTask.points"
          @keydown.esc="escapeEdit"
        />
      </form>
    </td>
  </tr>
</template>

<script setup>
// emits and props
const emit = defineEmits(["edit"]);
const { task } = defineProps({
  task: {
    type: Object,
    required: true,
  },
});

// Variables
const editedTask = ref({ ...task });

// Functions
const submitEdit = (event) => {
  if (JSON.stringify(editedTask) !== JSON.stringify(task)) {
    emit("edit", editedTask.value);
  }
  document.activeElement.blur();
};

const escapeEdit = (event) => {
  editedTask.value = { ...task };
  document.activeElement.blur();
};
</script>

<style scoped>
input {
  width: 100%;
  background-color: inherit;
  border: none;
  font: inherit;
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
