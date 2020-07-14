<template>
  <div>
    <h2>Todos</h2>
    <router-link to="/" class="home-link">Home</router-link>
    <hr />
    <AddTodo @add-todo="addTodo" />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
    <hr />
    <Loader v-if="loading" />
    <TodoList
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
      v-else-if="todos.length"
    />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'

export default {
  name: 'App',
  data() {
    return {
      todos: [
        { id: 1454545, title: 'Купить хлеб', completed: false },
        { id: 245454, title: 'Купить сыр', completed: false },
        { id: 3545454, title: 'Купить молоко', completed: false }
      ],
      loading: true,
      filter: 'all'
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
        this.todos.push(json)
        this.todos = this.todos.flat()
        this.loading = false
      })
  },
  // watch: {
  //   filter(value) {
  //     console.log(value)
  //   }
  // },
  computed: {
    filteredTodos() {
      switch (this.filter) {
        case 'all':
          return this.todos
        case 'completed':
          return this.todos.filter(todo => todo.completed)
        case 'not-completed':
          return this.todos.filter(todo => !todo.completed)
      }
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    addTodo(todo) {
      this.todos.unshift(todo)
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  }
}
</script>

<style lang="sass" scope>
hr
  width: 100%
  max-width: 720px
  margin: 20px auto
  border: 1px dashed

.home-link
  display: block
  padding-bottom: 10px

select
  margin-top: 10px
  border: 1px solid #ccc
  border-radius: 5px
  padding: 5px
  font-size: 1rem
</style>
