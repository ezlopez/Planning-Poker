<template>
  <ul>
    <li v-for="p in participants">
      <button
        v-show="isAdmin"
        class="delete-user-btn"
        @click="deleteUser(p.id)"
      >
        🗑️</button
      >{{ p.name }}
    </li>
  </ul>
</template>

<script setup>
const emit = defineEmits(["delete"]);

const { participants, isAdmin } = defineProps({
  participants: {
    type: Array,
    required: true,
  },
  isAdmin: {
    type: Boolean,
    required: true,
  },
});

const deleteUser = (userId) => {
  // console.log("Delete user: " + userId);
  emit("delete", userId);
};
</script>

<style scoped>
.delete-user-btn {
  display: none;
}

li {
  display: flex;
  justify-content: flex-start;
  gap: 0.5rem;
}

li:hover .delete-user-btn {
  display: block;
}
.delete-user-btn:hover {
  cursor: pointer;
}
</style>
