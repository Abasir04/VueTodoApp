<template>
    <div class="todo-item"
    :class="{'is-completed':todo.completed}">
        <p>
            <input type="checkbox" @change="markComplete">
            {{ todo.title }}
            <button @click="delTodo">X</button>
        </p>
    </div>
</template>

<script>
export default {
    name: 'TodoItem',
    props: ['todo'],
    emits: ['del-Todo'],
    methods: {
        markComplete() {
            // eslint-disable-next-line vue/no-mutating-props
            this.todo.completed = !this.todo.completed
        },
        delTodo() {
            this.$emit('del-todo', this.todo.id)
        }

    }
} 
</script>

<style scoped>

</style>