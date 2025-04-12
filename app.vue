<script setup>
import {ref} from 'vue'

let id = 0

const newTodo = ref('')
const todos = ref([
  {id: id++, text: 'Learn HTML'},
  {id: id++, text: 'Learn JavaScript'},
  {id: id++, text: 'Learn Vue'}
])

function addTodo() {
  if (newTodo.value !== '') {
    todos.value.push({id: id++, text: newTodo.value})
    newTodo.value = ''
  }
}

function removeTodo(todo) {
  todos.value = todos.value.filter(item => item !== todo)
}

</script>

<template>
  <div id="app">
    <v-form @submit.prevent="addTodo">
      <v-text-field v-model="newTodo" required placeholder="new todo"></v-text-field>
      <v-btn @click="addTodo">Add Todo</v-btn>
    </v-form>
    <ul>
      <v-list v-for="todo in todos" :key="todo.id">
        {{ todo.text }}
        <v-btn @click="removeTodo(todo)">X</v-btn>
      </v-list>
    </ul>
  </div>
</template>

<style>
#app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
}
</style>