<template>
  <div>
    <header>
      <img src="./assets/pinia-logo.svg" alt="Pinia Logo" />
      <h1>Pinia Tasks</h1>
    </header>

    <div class="task-list">
      <div v-for="task in taskStore.tasks">
        <TaskDetails :task="task" />
      </div>
    </div>
  </div>
</template>

<script>
import TaskDetails from './components/TaskDetails.vue';
import { useTaskStore } from './stores/TaskStore'

export default {
  components: { TaskDetails },
  setup() {
    const taskStore = useTaskStore()

    return { taskStore }
  }
}
</script>