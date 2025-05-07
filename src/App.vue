<template>
  <div class="todo-container">
    <h1>Daftar Kegiatan Saya</h1>
    <div class="input-group">
      <input type="text" v-model="newTask" placeholder="Tambahkan Kegiatan..." />
      <button @click="addTask">Tambahkan Kegiatan</button>
    </div>
    <ul class="task-list">
      <li v-for="(task, index) in tasks" :key="index">
        {{ task.text }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from "vue";

const newTask = ref("");
const tasks = ref([]);

const addTask = () => {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value });
    newTask.value = "";
  }
};
</script>
