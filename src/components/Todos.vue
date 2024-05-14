<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div>
        <!--eslint-disable-next-line vue/require-v-for-key--> 
        <div :key="todo.id" v-for="todo in todos">
            <TodoItem 
                :todo="todo"
                @del-todo="$emit('delTodo', todo.id)"
            />
                <!--  -->
        </div>
    </div>
</template>

<script>
import TodoItem from './TodoItems.vue'

export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Todos',
    props: ['todos'],
    components: {
        TodoItem
    }
}
</script>

<style scoped>

</style>
