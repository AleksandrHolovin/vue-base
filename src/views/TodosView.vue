<template>
    <div>
        <router-link to="/">Home</router-link>
        <hr />
        <AddTodo @add-todo="addTodo" />
        <select v-model="filter">
            <option value="all">All</option>
            <option value="completed">Completed</option>
            <option value="uncompleted">Uncompleted</option>
        </select>
        <Loader v-if="loading" />
        <TodoList v-else-if="todoItems.length" v-bind:todoItems="filteredTodos" @remove-todo="removeTodo" />
        <p v-else>No todos</p>
    </div>
</template>

<script lang="ts">
import TodoList from "@/components/TodoList.vue";
import AddTodo from '@/components/AddTodo.vue';
import Loader from '@/components/Loader.vue';

export default {
    name: "app",
    components: {
        TodoList,
        AddTodo,
        Loader,
    },
    // watch: {
    //     filter(value: any) {

    //     },
    // },
    computed: {
        filteredTodos() {
            if (this.filter === 'all') {
                return this.todoItems
            }
            if (this.filter === 'completed') {
                return this.todoItems.filter(todo => todo.completed)
            }
            if (this.filter === 'uncompleted') {
                return this.todoItems.filter(todo => !todo.completed)
            }
        }
    },
    methods: {
        removeTodo(id: number) {
            this.todoItems = this.todoItems.filter(todo => todo.id != id)
        },
        addTodo(newTodo: any) {
            this.todoItems = [...this.todoItems, newTodo]
        }
    },
    mounted() {
        this.loading = true;
        fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
            .then(response => response.json())
            .then(json => {
                this.todoItems = json;
                this.loading = false;
            })
    },
    data() {
        return {
            todoItems: [] as any[],
            loading: false,
            filter: 'all'
        }
    }
};
</script>