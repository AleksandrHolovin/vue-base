<template>
  <div id="app">
    <h1>Todo list</h1>
    <router-view />
  </div>
</template>

<script lang="ts">
import TodoList from "@/components/TodoList.vue";
import AddTodo from '@/components/AddTodo.vue';

export default {
  name: "app",
  components: {
    TodoList,
    AddTodo,
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
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => this.todoItems = json)
  },
  data() {
    return {
      todoItems: [] as any[]
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
