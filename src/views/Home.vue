<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos :todos="todos" />
  </div>
</template>

<script>
import Todos from '../components/Todos'
import AddTodo from '../components/AddTodo'
import { eventBus } from '../main'

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data () {
    return {
      todos: []
    }
  },

  // Life cycle hook - runs while the component creates
  created() {
    eventBus.$on('del-todo', index => {
      this.todos = this.todos.filter(todo => todo.id !== index)
      this.saveTodo()
    })
  },

  // Life cycle hook - runs as soon as components mounted to the DOM
  mounted() {
    if (localStorage.getItem('todos')) {
      try {
        this.todos = JSON.parse(localStorage.getItem('todos'));
      } catch(e) {
        localStorage.removeItem('todos');
      }
    }
  },

  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
      this.saveTodo()
    },
    addTodo(newTodo) {
      // this.todos = [...this.todos, newTodo]
      this.todos.push(newTodo)
      this.saveTodo()
    },

    // Local Storage to save data in browser  
    saveTodo() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem('todos', parsed);
    }
  }
}
</script>
