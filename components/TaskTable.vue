<template>
  <table>
    <thead>
      <tr>
        <th scope="col">Name</th>
        <th scope="col">Points</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="task in tasks" :key="task.id">
        <td><input type="text" :value="task.name" /></td>
        <td>{{ task.points }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
const props = defineProps({
  tasks: {
    type: Object,
    required: true,
  },
});

const tasks = reactive(props.tasks);
</script>

<style scoped>
input {
  width: 100%;
  background-color: inherit;
  border: none;
  font: inherit;
}
</style>
