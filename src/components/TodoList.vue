<template>
    <div class="container">
      <h1 class="title">Service Motor</h1>
      <input v-model="newTask" class="input" placeholder="Tambahkan antrian" @keyup.enter="addTodo" />
      <button @click="addTodo" class="button">Masukkan</button>
      <ul class="todo-list">
        <li v-for="(todo, index) in todos" :key="index" class="todo-item">
          <span :class="{ 'completed-task': todo.completed }" class="todo-text">{{ todo.task }}</span>
          <div class="button-group">
            <button @click="toggleTodo(index)" class="toggle-button">
              {{ todo.completed ? 'Batalkan' : 'Selesai' }}
            </button>
            <button @click="removeTodo(index)" class="remove-button">Hapus</button>
          </div>
        </li>
      </ul>
      <p class="unfinished-count">Yang belum diservice: {{ unfinishedTodosCount }}</p>
    </div>
  </template>
  
  <script>
  import { ref, computed } from 'vue'
  import { useTodoStore } from '../stores/todostore.js'
  
  export default {
    setup() {
      const todoStore = useTodoStore()
      const newTask = ref('')
  
      const addTodo = () => {
        if (newTask.value.trim()) {
          todoStore.addTodo(newTask.value)
          newTask.value = ''
        }
      }
  
      const unfinishedTodosCount = computed(() => todoStore.unfinishedTodosCount)
  
      return {
        newTask,
        todos: todoStore.todos,
        addTodo,
        removeTodo: todoStore.removeTodo,
        toggleTodo: todoStore.toggleTodo,
        unfinishedTodosCount
      }
    }
  }
  </script>
  
  <style scoped>
  .container {
    max-width: 500px;
    margin: 0 auto;
    padding: 30px;
    background-color: #282c34;
    border-radius: 10px;
    box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.3);
  }
  
  .title {
    color: #61dafb;
    margin-bottom: 25px;
    font-size: 28px;
    text-align: center;
    text-transform: uppercase;
  }
  
  .input {
    width: calc(100% - 110px);
    padding: 12px;
    border: 2px solid #61dafb;
    border-radius: 5px;
    margin-bottom: 20px;
    font-size: 18px;
    background-color: #fff;
    color: #282c34;
  }
  
  .button {
    width: 100px;
    padding: 12px;
    border: none;
    border-radius: 5px;
    background-color: #61dafb;
    color: #fff;
    font-size: 18px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .button:hover {
    background-color: #21a1f1;
  }
  
  .todo-list {
    list-style: none;
    padding: 0;
  }
  
  .todo-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 15px;
    padding: 10px;
    border-bottom: 1px solid #61dafb;
  }
  
  .todo-text {
    flex: 1;
    color: #fff;
  }
  
  .completed-task {
    text-decoration: line-through;
    color: #888;
  }
  
  .button-group {
    display: flex;
  }
  
  .toggle-button,
  .remove-button {
    padding: 8px 16px;
    margin-left: 10px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 14px;
    transition: background-color 0.3s;
  }
  
  .toggle-button {
    background-color: #28a745;
    color: #fff;
  }
  
  .toggle-button:hover {
    background-color: #218838;
  }
  
  .remove-button {
    background-color: #dc3545;
    color: #fff;
  }
  
  .remove-button:hover {
    background-color: #c82333;
  }
  
  .unfinished-count {
    color: #61dafb;
    margin-top: 20px;
    font-size: 18px;
    text-align: center;
  }
  </style>
  