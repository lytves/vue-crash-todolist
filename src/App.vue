<template>
    <div id="app">
        <Header></Header>
        <AddTodo v-on:add-todo="addTodo"></AddTodo>
        <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"></Todos>
    </div>
</template>

<script>
    import Header from "@/components/layout/Header.vue"
    import Todos from "@/components/Todos.vue"
    import AddTodo from "@/components/AddTodo.vue"

    export default {
        name: 'app',
        components: {
            Header,
            Todos,
            AddTodo
        },
        data() {
            return {
                todos: [
                    {
                        id: 1,
                        title: "Todo One",
                        completed: false
                    },
                    {
                        id: 2,
                        title: "Todo Two",
                        completed: true
                    },
                    {
                        id: 3,
                        title: "Todo Three",
                        completed: false
                    }
                ]
            }
        },
        methods: {
            deleteTodo(id) {
                this.todos = this.todos.filter(todo => todo.id !== id);
            },
            addTodo(newTodo) {
                this.todos = [...this.todos, newTodo];
            }
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
