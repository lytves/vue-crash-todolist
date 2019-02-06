<template>
    <div id="app">
        <AddTodo v-on:add-todo="addTodo"></AddTodo>
        <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"></Todos>
    </div>
</template>

<script>
    import axios from 'axios';
    import Todos from "@/components/Todos.vue";
    import AddTodo from "@/components/AddTodo.vue";

    export default {
        name: 'Home',
        components: {
            Todos,
            AddTodo
        },
        data() {
            return {
                todos: []
            }
        },
        methods: {
            deleteTodo(id) {
                axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                    .then(response => this.todos = this.todos.filter(todo => todo.id !== id))
                    .catch(err => console.log(err));
            },
            addTodo(newTodo) {
                const {title, completed} = newTodo;

                axios.post('https://jsonplaceholder.typicode.com/todos',
                    {
                        title,
                        completed
                    })
                    .then(response => this.todos = [...this.todos, response.data])
                    .catch(err => console.log(err));
            }
        },
        created() {
            // we will dump a json with some fake data
            axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
                .then(response => {
                    // JSON responses are automatically parsed
                    this.todos = response.data
                })
                .catch(err => console.log(err));
        }
    }
</script>

<style>
    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    body {
        font-family: Arial, Helvetica, sans-serif;
        line-height: 1.4;
    }
</style>
