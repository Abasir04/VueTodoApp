<template>
    <div class="bg-gray-200 p-2.5 border-b border-gray-300 border-dotted"
    :class="{'is-completed':todo.completed}">
        <p>
            <input class="mr-2" type="checkbox" @change="markComplete">
            {{ todo.title }}
            <button @click="delTodo" class="bg-red-600 text-white border-none py-0 px-2 rounded-full float-right cursor-pointer">X</button>
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
.is-completed {
    text-decoration: line-through;
}
</style>