<template>
    <div>
        <form @submit.prevent="addTodo" class="flex">
            <input 
                type="text" 
                name="title" 
                v-model='title'
                placeholder="AddTodo..."
                class="p-2 focus:outline-none border-b"
            >
            <input 
                type="submit" 
                value="SUBMIT"
                class="inline-block bg-gray-700 border-none text-white py-2 px-5 cursor-pointer hover:bg-gray-900"
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
    input[type="text"] {
        flex: 10;
    }
    input[type="submit"] {
        flex: 2;
    }
</style>