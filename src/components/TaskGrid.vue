<template>
  <div class="task-grid">
    <template v-if="tasks.length">
      <Task
        v-for="(task, i) in tasks"
        :key="task.name"
        :task="task"
        @deleted="$emit('deleted', i)"
        @state="$emit('state', i)"
      ></Task>
    </template>
    <template v-else>
      <p class="no-task">Sua vida esta em dia :)</p>
    </template>
  </div>
</template>

<script>
import Task from './Task.vue';

export default {
  components: { Task },
  props: {
    tasks: { type: Array, required: true }
  }
}
</script>

<style>
.task-grid {
  margin-top: 50px;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.task-grid .task {
  margin: 15px;
}
</style>