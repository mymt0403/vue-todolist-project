<template>
  <div class="container">
    <h1>ToDo List</h1>
    <TaskInput @add-task="addTask" />
    <TaskList :tasks="tasks" @delete-task="deleteTask" />
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import TaskInput from './components/TaskInput.vue'
import TaskList from './components/TaskList.vue'

const tasks = reactive([])
const addTask = (text) => {
  tasks.push({ text, completed: false, editing: false })
}
const deleteTask = (index) => {
  tasks.splice(index, 1)
}
</script>

<style scoped>
h1 {
    text-align: center;
}

.container {
  max-width: 500px;
  margin: 2rem auto;
  font-family: sans-serif;
}
</style>
