<template>
    <div>
        <input v-model="newTodoText" v-on:keyup.enter="addNewTodo" placeholder="Add a todo">
        <ul>
            <li is="todo-item" v-for="(todo, index) in todos" v-bind:title="todo" v-on:remove="todos.splice(index, 1)"></li>
        </ul>
    </div>
</template>
<script>
    import Vue from 'vue'
    export default {
        name: 'TodoList',
        data: function() {
            return {
                newTodoText: '',
                todos: [
                    'Do the dishes',
                    'Take out the trash',
                    'Mow the lawn'
                ]
            }
        },
        methods: {
            addNewTodo: function() {
                this.todos.push(this.newTodoText)
                this.newTodoText = ''
            }
        }
    }
    Vue.component('todo-item', {
        template: '\
            <li>\
            {{ title }}\
            <button v-on:click="$emit(\'remove\')">X</button>\
            </li>\
        ',
        props: ['title']
    })
</script>
<style scoped>
    li {
        text-align: left;
    }
</style>