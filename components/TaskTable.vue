<template>
  <table>
    <thead>
      <tr>
        <th scope="col">Name</th>
        <th scope="col">Points</th>
      </tr>
    </thead>
    <tbody>
      <TaskRow
        v-for="task in tasks"
        :task="task"
        @edit="taskEdit"
        @vote="taskVote"
      />
    </tbody>
  </table>
</template>

<script setup>
const emit = defineEmits(["task-edit", "task-vote"]);
const { tasks } = defineProps({
  tasks: {
    type: Object,
    required: true,
  },
});

function taskEdit(task) {
  emit("task-edit", task);
}

function taskVote(taskId) {
  emit("task-vote", taskId);
}
</script>
