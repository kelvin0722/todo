<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import axios from 'axios'

import Todos from './components/Todos'
import Header from './components/Layout/Header'
import AddTodo from './components/AddTodo'

export default {
  name: 'app',
  components: {
    Header,
    AddTodo,
    Todos,
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    async deleteTodo(id){
      try {
        const response = await axios.delete('https://jsonplaceholder.typicode.com/', id)
        this.todos = this.todos.filter(todo => todo.id !== response.data.id )
      } catch (error) {
        console.log(error)
      }
    },
    async addTodo(newTodo){
      try {
        const { title , completed } = newTodo
        const response = await axios.post('https://jsonplaceholder.typicode.com/', {
          title,
          completed
        })
      } catch (error) {
        console.log(error)
      }
        this.todos = [...this.todos, response.data]
    },
  },
  async created() {
    try {
      const response = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      this.todos = response.data
    } catch (error) {
      console.log(error)
    }
  },
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover{
    background: #666;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
</style>
