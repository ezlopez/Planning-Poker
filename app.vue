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
    <section v-if="!isVoting" class="task-list">
      <h2>Tasks</h2>
      <TaskTable
        :tasks="tasks"
        @task-edit="submitTaskEdit"
        @task-vote="launchTaskVote"
      />
    </section>

    <section v-if="isVoting" class="voting-section">
      <h2>Voting</h2>
      <VotingBooth :task="taskToVoteOn" @cast="castVote" />
    </section>

    <section class="voter-list">
      <h2>Voters</h2>
      <ParticipantList
        :participants="participants"
        :isAdmin="localUser.isAdmin"
        @delete="deleteParticipant"
      />
    </section>
  </main>

  <dialog id="new-user-dialog">
    <form method="dialog">
      <h3>Set your username:</h3>
      <input
        type="text"
        v-model="newUsername"
        pattern="[a-zA-Z0-9_]{1,32}"
        title="[a-zA-Z0-9_]{1,32}"
      />
      <button @click="saveUsername">OK</button>
    </form>
  </dialog>

  <footer>
    <p>Made by Zeke :)</p>
  </footer>
</template>

<script setup>
const tasks = ref([]);
const participants = ref([]);
const newUsername = ref("New_User");
const isVoting = ref(false);
const taskToVoteOn = ref(null);

const localUser = useCookie("localUser", {
  default: () => {
    return {
      name: "New_User",
      id: uuidv4(),
      isAdmin: false,
      isNew: true,
    };
  },
  sameSite: true,
});

const saveUsername = () => {
  localUser.value.name = newUsername;
  localUser.value.isNew = false;
};

const handleUserUpdate = (newSettings) => {
  localUser.value.name = newSettings.name;
  localUser.value.isAdmin = newSettings.isAdmin;
};

const deleteParticipant = (id) => {
  participants.value = participants.value.filter((p) => p.id != id);
};

const submitTaskEdit = (editedTask) => {
  const taskIndex = tasks.value.findIndex((task) => task.id === editedTask.id);
  tasks.value[taskIndex] = { ...editedTask };
};

const launchTaskVote = (taskId) => {
  isVoting.value = true;
  taskToVoteOn.value = { ...tasks.value.find((task) => task.id === taskId) };
};

const castVote = (taskId, voteValue) => {
  console.log(`Casting vote of ${voteValue} points for ${taskId}`);
};

function uuidv4() {
  return "10000000-1000-4000-8000-100000000000".replace(/[018]/g, (c) =>
    (
      c ^
      (crypto.getRandomValues(new Uint8Array(1))[0] & (15 >> (c / 4)))
    ).toString(16)
  );
}

onMounted(() => {
  // ********* New user check *********
  if (localUser.value.isNew) {
    const dialog = document.getElementById("new-user-dialog");
    dialog.addEventListener("cancel", (event) => {
      event.preventDefault();
    });
    dialog.showModal();
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
});
</script>

<style>
@import url("~/public/style.css");

#new-user-dialog {
  position: absolute;
  top: 5rem;
  margin: auto;
  border: 2px solid black;
  padding: 1rem;
  text-align: center;
}

#new-user-dialog::backdrop {
  background-color: rgba(0, 0, 0, 0.8);
}

#new-user-dialog h3 {
  margin-bottom: 1rem;
}

#new-user-dialog input {
  font: inherit;
}

#new-user-dialog button {
  font: inherit;
  margin-left: 1rem;
}
</style>
