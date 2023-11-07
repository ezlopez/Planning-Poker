<template>
  <table>
    <thead>
      <tr>
        <th scope="col">Name</th>
        <th scope="col">Points</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="task in tasks">
        <td>{{ task.name }}</td>
        <td>{{ task.points }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
const { tasks } = defineProps({
  tasks: {
    type: Object,
    required: true,
  },
});
</script>
