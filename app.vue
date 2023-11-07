<template>
  <header>
    <img
      src="planning-poker-white-svgrepo-com.svg"
      alt="Poker Planning Icon"
      class="header-pp-icon"
    />
    <h1>Planning Poker</h1>
    <button class="user-corner" id="user-corner" @click="openDialog">
      <img
        src="user-circle-svgrepo-com.svg"
        alt="User Profile Icon"
        class="header-user-icon"
      />
      <p>{{ localUser.name }}</p>
    </button>
  </header>

  <main>
    <section class="task-list">
      <h1>Tasks</h1>
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
    </section>

    <section class="voter-list">
      <h1>Voters</h1>
      <ul>
        <li v-for="voter in voters">
          <button v-if="localUser.isAdmin">🗑️</button>{{ voter.name }}
        </li>
      </ul>
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
var voters = ref([]);
var localUser = ref({
  name: "Username",
  id: uuidv4(),
  isAdmin: true,
});

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
  tasks.value.push({ name: "Some task " + i + " - Do a thing", points: 0 });
}

voters.value = [
  { name: "Alice", id: uuidv4(), isAdmin: false },
  { name: "Bob", id: uuidv4(), isAdmin: false },
  { name: "Cecilia", id: uuidv4(), isAdmin: false },
  { name: "David", id: uuidv4(), isAdmin: false },
  { name: "Erica", id: uuidv4(), isAdmin: false },
  { name: "Frank", id: uuidv4(), isAdmin: false },
];
</script>
