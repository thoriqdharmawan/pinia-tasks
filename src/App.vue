<template>
  <main>
    <header>
      <img src="./assets/pinia-logo.svg" alt="Pinia Logo" />
      <h1>Pinia Tasks</h1>
    </header>

    <div class="new-task-form">
      <TaskForm />
    </div>

    <div class="loading" v-if="loading">Loading tasks...</div>

    <nav class="filter">
      <button @click="filter = 'all'">All tasks </button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ totalCount }} task left to do</p>
      <div v-for="task in tasks">
        <TaskDetails :task="task" />
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ favCount }} task left to do</p>
      <div v-for="task in favs">
        <TaskDetails :task="task" />
      </div>
    </div>

    <div class="reset">
      <button @click="taskStore.$reset">Reset state</button>
    </div>
  </main>
</template>

<script>
import { ref } from 'vue';
import TaskDetails from './components/TaskDetails.vue'
import { useTaskStore } from './stores/TaskStore'
import TaskForm from './components/TaskForm.vue'
import { storeToRefs } from 'pinia';


export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStore = useTaskStore()

    const { tasks, loading, totalCount, favCount, favs } = storeToRefs(taskStore)

    taskStore.getTasks()

    const filter = ref('all')

    return { taskStore, filter, tasks, loading, totalCount, favCount, favs }
  }
}
</script>