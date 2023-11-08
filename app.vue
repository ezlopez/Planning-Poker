<template>
  <header>
    <img
      src="planning-poker-white-svgrepo-com.svg"
      alt="Planning Poker Icon"
      class="header-pp-icon"
      width="100"
      height="100"
    />
    <h1>Planning Poker</h1>
    <UserCorner :user="localUser" @update="handleUserUpdate" />
  </header>

  <main>
    <section class="task-list">
      <h1>Tasks</h1>
      <TaskTable :tasks="tasks" />
    </section>

    <section class="voter-list">
      <h1>Voters</h1>
      <ParticipantList :participants="participants" :isAdmin="false" />
    </section>
  </main>

  <footer>
    <p>Made by Zeke</p>
  </footer>
</template>

<style>
@import url("~/public/style.css");
</style>

<script setup>
var tasks = ref([]);
var participants = ref([]);
var localUser = ref({
  name: "Username",
  id: uuidv4(),
  isAdmin: true,
});

const handleUserUpdate = (newSettings) => {
  console.log(newSettings);
  localUser.value.name = newSettings.name;
  localUser.value.isAdmin = newSettings.isAdmin;
};

function uuidv4() {
  return "10000000-1000-4000-8000-100000000000".replace(/[018]/g, (c) =>
    (
      c ^
      (crypto.getRandomValues(new Uint8Array(1))[0] & (15 >> (c / 4)))
    ).toString(16)
  );
}

// ********* Adding fake data *********
for (var i = 1; i <= 30; i++) {
  tasks.value.push({
    name: "Some task " + i + " - Do a thing",
    points: 0,
    id: uuidv4(),
  });
}

participants.value = [
  { name: "Alice", id: uuidv4(), isAdmin: false },
  { name: "Bob", id: uuidv4(), isAdmin: false },
  { name: "Cecilia", id: uuidv4(), isAdmin: false },
  { name: "David", id: uuidv4(), isAdmin: false },
  { name: "Erica", id: uuidv4(), isAdmin: false },
  { name: "Frank", id: uuidv4(), isAdmin: false },
];
</script>
