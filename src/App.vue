<template>
  <div :class="['todo-container', { dark: isDarkMode }]">
    <div class="dark-mode-toggle">
      <label class="switch">
        <input type="checkbox" v-model="isDarkMode" />
        <span class="slider"></span>
      </label>
      <span>{{ isDarkMode ? "🌙 Dark Mode" : "🌞 Light Mode" }}</span>
    </div>
    <h1>Daftar Kegiatan Saya</h1>
    <div class="input-group">
      <input type="text" v-model="newTask" placeholder="Tambahkan Kegiatan..." />
      <button @click="addTask">Tambahkan Kegiatan</button>
    </div>
    <div class="filter-group">
      <label>
        <input type="checkbox" v-model="showOnlyIncomplete" />
        Tampilkan Hanya Yang Belum Selesai
      </label>
    </div>
    <ul class="task-list">
      <li v-for="(task, index) in filteredTasks" :key="index">
        <label>
          <input type="checkbox" v-model="task.completed" />
          <span :class="{ done: task.completed }">{{ task.text }}</span>
        </label>
        <button @click="removeTask(index)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const newTask = ref("");
const tasks = ref([]);
const showOnlyIncomplete = ref(false);
const isDarkMode = ref(false);

const addTask = () => {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value, completed: false });
    newTask.value = "";
  }
};

const removeTask = (index) => {
  tasks.value.splice(index, 1);
};

const filteredTasks = computed(() => {
  return showOnlyIncomplete.value
    ? tasks.value.filter((task) => !task.completed)
    : tasks.value;
});
</script>
