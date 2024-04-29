<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div>
    <h1>To-Do List</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Tambah kegiatan">
    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index">
        <input type="checkbox" v-model="task.completed">
        <span :class="{ 'completed': task.completed }">
          {{ task.name }}
        </span>
        <button @click="cancelTask(index)">Batal</button>
        
      </li>
    </ul>
    <button @click="filterCompleted">{{ showCompleted ? 'Sembunyikan' : 'Tampilkan' }} yang belum selesai</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
      showCompleted: false
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ name: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    cancelTask(index) {
      this.tasks.splice(index, 1);
    },
    filterCompleted() {
      this.showCompleted = !this.showCompleted;
    }
  },
  computed: {
    filteredTasks() {
      return this.showCompleted ? this.tasks.filter(task => !task.completed) : this.tasks;
    }
  }
}
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>

