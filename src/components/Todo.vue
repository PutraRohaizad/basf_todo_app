<template>
  <div class="container">
    <h1>BASF Todo List</h1>
    <div class="input-group">
      <input v-model="todoTitle" placeholder="Title" />
    </div>
    <div class="input-group">
      <textarea v-model="todoDesc" placeholder="Description" cols="50" rows="5"></textarea>
    </div>
    <button @click="addTask">Add</button>
    <br>
    <hr>
    <br>
    <div class="search-group">
      <input v-model="searchQuery" placeholder="Search todo" />
    </div>

    <table>
      <thead>
        <tr>
          <th>#</th>
          <th>Task Title</th>
          <th>Task Description</th>
          <th>Status</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in filteredTasks" :key="index">
          <td>{{ index + 1 }}</td>
          <td :class="{ completed: task.completed }">            
            <b style="font-weight: bold !important;">{{ task.title }}</b>
            <p>{{ task.description }}</p>
          </td>
          <td>{{ task.completed ? '✅ Done' : '⏳ Pending' }}</td>
          <td>
            <button @click="removeTask(index)">❌</button>
            <button @click="updateTask(task)">✍🏻</button>
          </td>
        </tr>
      </tbody>
    </table>
    <br>
    <p v-if="filteredTasks.length === 0">No matching todo found.</p>

  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const todoTitle = ref('')
const todoDesc = ref('')
const tasks = ref([])
const searchQuery = ref('')


const addTask = () => {  
  if (todoTitle.value.trim() && todoDesc.value.trim()) {
    tasks.value.push({ title: todoTitle.value, description: todoDesc.value, completed: false })
    todoTitle.value = ''
    todoDesc.value = ''
  }else{
    alert('The task is empty .. please fill in something :)')
  }
}

const removeTask = (index) => {
  tasks.value = tasks.value.filter((task, i) => i != index)
}

const updateTask = (task) => {
  task.completed = !task.completed
}

// Computed property to filter tasks based on search input
const filteredTasks = computed(() => {
  return tasks.value.filter(task => 
    task.title.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
})

</script>

<style scoped>

.container {
  max-width: 500px;
  margin: 20px auto;
  text-align: center;
}
.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
input {
  flex: 1;
  padding: 8px;
}
button {
  padding: 8px;
  cursor: pointer;
  margin: 5px;
  width: 100%;
  background-color: rgb(26, 119, 126);
  color: white;
}
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}
th, td {
  border: 1px solid #ddd;
  padding: 10px;
  text-align: center;
}
th {
  background: #f4f4f4;
}
.completed {
  text-decoration: line-through;
  color: gray;
}
</style>
