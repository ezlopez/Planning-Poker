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
</template>

<script setup>
const { user } = defineProps({
  user: {
    type: Object,
    required: true,
  },
});

const openDialog = () => {
  console.log("Open user edit dialog.");
};
</script>
