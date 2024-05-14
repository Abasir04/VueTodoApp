<template>
    <div>
        <form @submit.prevent="addTodo">
            <input 
                type="text" 
                name="title" 
                v-model='title'
                placeholder="AddTodo..."
            >
            <input 
                type="submit" 
                value="Submit" 
                class="btn"
            >
        </form>
    </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid'

export default {
    name: 'AddTodo',
    emits: ['add-todo'],
    methods: {
        addTodo() {
            if (!this.title) return alert('Add a Todo') 
            const newTodo = {
                id: uuidv4(),
                title: this.title,
                completed: false
            }
            this.saveToLocalStorage({ title: this.title, completed: false })
            this.$emit('add-todo', newTodo)
            this.title = ''
        },
        saveToLocalStorage(todo) {
            const todos = JSON.parse(localStorage.getItem('todos')) || []
            todos.push(todo)
            localStorage.setItem('todos', JSON.stringify(todos))
        }
    },
    data() {
        return {
            title: ''
        }
    }
}
</script>

<style scoped>

</style>