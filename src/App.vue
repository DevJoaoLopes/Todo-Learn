<template>
  <div id="app">
    <h1>Lista de Tarefas</h1>
    <taskProgress :progress="progress" />
    <NewTask @taskAdded="addTask" />
    <TaskGrid :tasks="tasks" @state="changeState" @deleted="deleteTask"></TaskGrid>
  </div>
</template>

<script>
import TaskProgress from './components/TaskProgress.vue';
import TaskGrid from './components/TaskGrid.vue'
import NewTask from './components/NewTask.vue';

export default {
  components: { TaskProgress, TaskGrid, NewTask },
  data: () => ({
    tasks: [

    ]
  }),
  computed: {
    progress () {
      const total = this.tasks.length;
      const done = this.tasks.filter(t => !t.pending).length;
      return Math.round(done / total * 100) || 0;
    }
  },
  watch: {
    tasks: {
      deep: true,
      handler () {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      }
    }
  },
  methods: {
    addTask (task) {
      const sameName = t => t.name === task.name;
      const reallyNew = this.tasks.filter(sameName).length == 0;
      if (reallyNew) {
        this.tasks.push({
          name: task.name,
          pending: task.pending || true,
        })
      }
    },
    deleteTask (i) {
      this.tasks.splice(i, 1);
    },
    changeState (i) {
      this.tasks[i].pending = !this.tasks[i].pending;
    }
  },
  created () {
    const data = localStorage.getItem('tasks');
    this.tasks = JSON.parse(data) || [];
  }
};

</script>

<style>
body {
  background: #34e89e; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #0f3443,
    #34e89e
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #0f3443,
    #34e89e
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  font-family: "Lato", sans-serif;
  color: #ffffff;
}

#app {
  display: flex;
  flex: 1;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
}

#app h1 {
  margin-bottom: 5px;
  font-size: 3rem;
  font-weight: 300;
}
</style>
