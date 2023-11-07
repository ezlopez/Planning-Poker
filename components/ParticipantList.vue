<template>
  <ul>
    <li v-for="p in participants">
      <button v-if="isAdmin">🗑️</button>{{ p.name }}
    </li>
  </ul>
</template>

<script setup>
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
</script>
