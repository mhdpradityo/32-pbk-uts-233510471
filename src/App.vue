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
<style scoped>
.todo-container {
  max-width: 600px;
  margin: 2rem auto;
  padding: 2rem;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  font-family: sans-serif;
  background: #f9f9f9;
  color: #333;
}

.todo-container.dark {
  background-color: #1e1e2f;
  color: #e0e0e0;
}

h1 {
  text-align: center;
  margin-bottom: 1.5rem;
}

.input-group {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.input-group input {
  flex: 1;
  padding: 0.8rem;
  border: 1px solid #ccc;
  border-radius: 8px;
}

.input-group button {
  padding: 0.8rem 1rem;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}

.input-group button:hover {
  background-color: #2980b9;
}

.filter-group {
  margin-bottom: 1rem;
  font-size: 0.9rem;
  color: inherit;
}

.filter-group label {
  display: flex;
  align-items: center;
  gap: 0.4rem;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-list li {
  background: #fff;
  padding: 0.8rem 1rem;
  margin-bottom: 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
}

.todo-container.dark .task-list li {
  background-color: #2e2e42;
}

.task-list label {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.task-list input[type="checkbox"] {
  width: 20px;
  height: 20px;
}

.done {
  text-decoration: line-through;
  color: #888;
}

.todo-container.dark .done {
  color: #999;
}

.task-list button {
  background-color: #e74c3c;
  border: none;
  color: white;
  padding: 0.5rem 0.8rem;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.task-list button:hover {
  background-color: #c0392b;
}

.dark-mode-toggle {
  display: flex;
  align-items: center;
  gap: 1rem;
  justify-content: flex-end;
  margin-bottom: 1rem;
}

.switch {
  position: relative;
  display: inline-block;
  width: 46px;
  height: 24px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  background-color: #ccc;
  border-radius: 24px;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  transition: 0.4s;
}

.slider::before {
  position: absolute;
  content: "";
  height: 18px;
  width: 18px;
  border-radius: 50%;
  background-color: white;
  bottom: 3px;
  left: 3px;
  transition: 0.4s;
}

.switch input:checked + .slider {
  background-color: #3498db;
}

.switch input:checked + .slider::before {
  transform: translateX(22px);
}
</style>
