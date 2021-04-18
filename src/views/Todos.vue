<template>
  <div>
    <h2>Todo App</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo
    @add-todo='addTodo'
    />
    <br>
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    <hr>
    <Loader v-if='loading' />
    <TodoList
    v-else-if="filteredTodos.length"
    v-bind:todos="filteredTodos"
    @remove-todo='removeTodo'
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
        // {id:1, title: 'проснуться', completed: false},
        // {id:2, title: 'сварить кофе', completed: false},
        // {id:3, title: 'приготовить завтрак', completed: false},
        // {id:4, title: 'умыться', completed: false}
      ],
      loading:true,
      filter:'all'
    }

  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
  .then(response => response.json())
  .then(json => {
      setTimeout(() => {
this.todos=json
  this.loading = false
      }, 1000)
  })
  },
//   watch: {
// filter(value) {
  
// }
//   },
computed: {
  filteredTodos () {
    if (this.filter === 'all') {
      return this.todos
    }
     if (this.filter === 'completed') {
      return this.todos.filter(t=>t.completed)
    }
     if (this.filter === 'not-completed') {
      return this.todos.filter(t=>!t.completed)
    }

  }
},
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  }
}
</script>