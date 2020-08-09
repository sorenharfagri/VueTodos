<template>
    <div>
        <p>Todo list</p>
        <ul>
            <!--            Компонент отвечающий за один таск-->
            <!--            Принимает todo, и индекс в качестве его id-->
            <TodoItem
                    v-for="(todo, i) of todos"
                    :key="todo.id"
                    v-bind:todo="todo"
                    v-bind:index="i"
                    v-on:remove-todo="removeTodo"
            />
        </ul>
    </div>
</template>

<script>
    import TodoItem from "@/components/TodoItem";

    export default {
        props: ['todos'],
        components: {
            TodoItem
        },
        methods: {
            removeTodo(id) {
                this.$emit('remove-todo', id)
            }
        }
    }
</script>