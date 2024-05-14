<template>
  <div>
    <TodoHeader />
    <AddTodo 
      @add-Todo="addTodo"
    />
    <Todos 
      :todos="todos"
      @delTodo="deleteTodo"
    /> 
  </div>
</template>

<script>
import Todos from './components/Todos.vue'
import TodoHeader from './components/layout/Header.vue'
import AddTodo from './components/AddTodo.vue'

export default {
  name: 'App',
  components: {
    Todos, TodoHeader, AddTodo
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
      this.removeTodo(id)
    },
    addTodo(newTodo) {
      this.todos.push(newTodo)
      //this.todo = [...this.todo, newTodo]
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },
    removeTodo(id) {
      let todos = JSON.parse(localStorage.getItem('todos')) || [];
      todos = todos.filter(todo => todo.id !== id);
      localStorage.setItem('todos', JSON.stringify(todos));
    }
  },
  created() {
    this.todos = JSON.parse(localStorage.getItem('todos')) || []
  }
}
</script>

