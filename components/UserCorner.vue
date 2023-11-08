<template>
  <div class="user-corner" @click="openDialog">
    <img
      src="user-circle-svgrepo-com.svg"
      alt="User Profile Icon"
      class="header-user-icon"
    />
    <!-- <p>placeholder</p> -->
    <p>{{ user.name }}</p>
  </div>

  <dialog id="user-edit-dialog">
    <h2>Edit user settings</h2>
    <form method="dialog">
      <label for="username-edit">Username:</label>
      <input
        id="username-edit"
        v-model="editedValues.name"
        class="dialog-input-text"
        pattern="[a-zA-Z0-9_]{1,32}"
        title="[a-zA-Z0-9_]{1,32}"
      />
      <br />
      <input
        id="isAdmin-edit"
        type="checkbox"
        v-model="editedValues.isAdmin"
        class="dialog-input-checkbox"
      />
      <label for="isAdmin-edit">Admin</label>
      <br />
      <div class="dialog-footer">
        <button @click="submitValues">OK</button>
        <button>Cancel</button>
      </div>
    </form>
  </dialog>
</template>

<script setup>
const { user } = defineProps({
  user: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(["update"]);

const editedValues = ref({
  name: user.name,
  isAdmin: user.isAdmin,
});

const openDialog = () => {
  resetEditedValues();

  const dialog = document.getElementById("user-edit-dialog");
  dialog.showModal();
  dialog.addEventListener("cancel", (event) => {
    dialogCancel();
  });
};

const submitValues = () => {
  console.log("Submitting");
  emit("update", editedValues.value);
};

const resetEditedValues = () => {
  editedValues.value = {
    name: user.name,
    isAdmin: user.isAdmin,
  };
};
</script>

<style scoped>
dialog {
  position: absolute;
  top: 3rem;
  margin: 0 auto;
  padding: 2rem;
  max-width: 100vw;
  border: none;
  text-align: left;
}

dialog::backdrop {
  background-color: rgba(0, 0, 0, 0.8);
}

dialog h2 {
  margin-bottom: 1em;
  text-align: center;
}

dialog :is(button, input) {
  font: inherit;
}

.dialog-footer {
  width: 100%;
  display: flex;
  margin-top: 0.2rem;
  justify-content: flex-end;
  gap: 1rem;
}

.dialog-input-text {
  margin-left: 1rem;
  max-width: 8rem;
}

.dialog-input-checkbox {
  margin-right: 0.6rem;
  margin-top: 1rem;
}
</style>
