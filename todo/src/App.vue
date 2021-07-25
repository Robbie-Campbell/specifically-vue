<template>
  <div class="container">
    <div class="border p-4 mt-5">
      <header>
        <Header title="This is the title" />
      </header>
        <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue'
import 'bootstrap';
import 'bootstrap/dist/css/bootstrap.min.css';
export default {
  name: 'App',
  components: {
    Header,
    Tasks
  },
  data() {
    return {
      tasks: []
    }
  },
  methods: {
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id)
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => task.id === id ?
      {...task, reminder: !task.reminder} : task);
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors appointment',
        day: 'October 9th 2:30',
        reminder: true
      },
      {
        id: 2,
        text: 'Dentists appointment',
        day: 'January 9th 2:30',
        reminder: true
      },
      {
        id: 3,
        text: 'Fishing Trip',
        day: 'January 9th 2:30',
        reminder: false
      }
    ]
  }
}
</script>