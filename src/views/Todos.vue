<template>
    <div>
        <h2>Todo application</h2>
        <router-link to="/">Home</router-link>
        <hr>
        <!--        Добавление нового таска-->
        <AddTodo
                @add-todo="addTodo"
        />
        <!--  Фильтрация todos-->
        <select v-model="filter">
            <option value="all">All</option>
            <option value="completed">Completed</option>
            <option value="not-completed">Not Completed</option>
        </select>
        <hr>
        <!--        Круг загрузки, применяется во время загрузки данных с сервера-->
        <Loader v-if="loading"/>
        <!--        Список тасков, отображается если есть таски, в ином случае, отображает надпись "No todos"-->
        <!--        Принимает вычисляемое свойство filteredTodos, которое содержит в себе список отфильтрованных тасков -->
        <TodoList
                v-else-if="filteredTodos.length"
                v-bind:todos="filteredTodos"
                @remove-todo="removeTodo"
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
                //Массив самих todos
                //@title: string
                //@completed: boolean
                todos: [],
                // Стейт, отвечающий за отображение компонента Loading, во время загрузки todos с сервера
                loading: true,
                // Стейт, отвечающий за фильтрацию todos, связан моделью с селектом, имеет три состояния - all, completed, not-completed
                // TodoList использует вычисляемое свойство filtredList, на основе filter
                filter: 'all'
            }
        },

        //AddTodo - Добавление нового таска
        //Loader - Кружок загрузки, отображающийся во время загрузки данных с сервера
        components: {
            TodoList, AddTodo, Loader
        },
        mounted() {
            //Добываем todos в массив todos
            //После загрузки данных loading устанавливается в false, тем самым, круг загрузки пропадает
            fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
                .then(response => response.json())
                .then(json => {
                    setTimeout(() => {
                        this.todos = json
                        this.loading = false;
                    }, 1000)
                })
        },
        computed: {
            //Вычисляемое свойство для фильтрации todos
            //Содержит в себе отфильтрованные таски
            //Взаимосвязан с filter, который содержит в себе статус фильтрации
            //all - отображать вес таски
            //completed - отображать выполненные таски
            //not-completed - отображать невыполнненые таски
            filteredTodos() {
                switch (this.filter) {
                    case "all" :
                        return this.todos;
                    case "completed" :
                        return this.todos.filter(todo => todo.completed);
                    case "not-completed" :
                        return this.todos.filter(todo => !todo.completed);
                    default:
                        return this.todos;
                }

            }
        },
        methods: {
            removeTodo(id) {
                this.todos = this.todos.filter(todo => todo.id !== id)
            },
            addTodo(todo) {
                this.todos.push(todo)
            }
        }
    }
</script>