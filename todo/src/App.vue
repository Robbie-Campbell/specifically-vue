<template>
  <div class="container">
    <div class="border p-4 mt-5">
      <header>
        <Header @toggle-add-task="toggleAddTask"
         title="This is the title" :showAddTask="showAddTask" />
        <div v-show="showAddTask">
          <AddTask @add-task="addTask" />
        </div>
      </header>
        <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'
import 'bootstrap';
import 'bootstrap/dist/css/bootstrap.min.css';
export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    async addTask(task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task),
      })
      const data = await res.json();
      this.tasks = [...this.tasks, data]
    },
    async deleteTask(id) {
      const res = await fetch(`api/tasks/${id}`, {
        method: 'DELETE'
      });
      res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert("Error Deleting Task");
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id);
      const updTask = {...taskToToggle, reminder: !taskToToggle.reminder};

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updTask),
      });

      const data = await res.json();
      this.tasks = this.tasks.map((task) => task.id === id ?
      {...task, reminder: data.reminder} : task);
    },
    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    }
  },
  async created() {
    this.tasks = await this.fetchTasks();
  }
}
</script>