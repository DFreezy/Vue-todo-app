<template>
  <div class="app">
    <h1>📃 Vue To-Do List</h1>
    <form @submit.prevent="addTodo">
      <input v-model="newTodo" placeholder="Enter a task"/>
      <button>Add</button>
    </form>

    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <span :class="{done: todo.done}"
        @click="toggleDone(index)">
      {{ todo.text }}
      </span>
      <button @click="removeTodo(index)">
        ❌
      </button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import {ref} from 'vue'

const newTodo = ref('')
const todos = ref([])

function addTodo() {
  if(newTodo.value.trim() !== ''){
    todos.value.push({text: newTodo.value, done: false})
    newTodo.value = ''
  }
}

function toggleDone(index){
  todos.value[index].done = !
  todos.value.splice(index, 1)
}
</script>

<style scoped>
.app{
  max-width: 500px;
  margin: auto;
  text-align: center;
  font-family: Arial, sans-serif;
}

input{
  padding: 10px;
  width: 60%;
  margin-right: 10px;
}

button {
  padding: 10px;
  cursor: pointer;
}

ul{
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
  background: #f3f3f3;
  padding: 10px;
  border-radius: 5px;
}

.done {
  text-decoration: line-through;
  color: gray;
}
</style>