<!--Компонент отвечающий за один таск-->

<template>
    <li>
        <!--        Если таск завершён - будет присвоен класс done, который зачеркивает обозначит законченный такс-->
        <span v-bind:class="{done: todo.completed}">
<!--            Чекбокс, отвечающий за состояние таска (Выполнен ли)-->
            <input type="checkbox" v-on:change="todo.completed = !todo.completed">
            <!--            id чекбокса-->
            <strong>{{index + 1}}</strong>
            {{todo.title | uppercase}}
        </span>
        <!--        Кнопка удаления таска, при нажатии задействуется метод родителя, которая исключит таск из массива тасков-->
        <!--        Таск идентифицируется в массиве с помощью его id-->
        <button class="rm" v-on:click="$emit('remove-todo', todo.id)">&times;</button>
    </li>
</template>

<script>
    export default {
        props: {
            todo: {
                type: Object,
                required: true
            },
            index: Number
        },
        filters: {
            uppercase(value) {
                return value.toUpperCase()
            }
        }
    }
</script>

<style scoped>
    ul {
        list-style: none;
        maring: 0;
        padding: 0;
    }

    li {
        border: 1px solid #ccc;
        display: flex;
        justify-content: space-between;
        padding: .5rem 2rem;
        margin-bottom: 1rem;
    }

    .rm {
        background: red;
        color: #fff;
        border-radius: 50%;
        font-weight: bold;
    }

    input {
        margin-right: 1rem;
    }

    .done {
        text-decoration: line-through
    }

</style>