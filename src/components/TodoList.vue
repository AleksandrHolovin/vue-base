<template>
  <div>
    <ul>
      <TodoItem v-for="(todo, index) of todoItems" v-bind:todo="todo" v-bind:index="index" @remove-todo="removeTodo" />
    </ul>
  </div>
</template>

<script lang="ts">
import TodoItem from '@/components/TodoItem.vue';

export default {
  props: ['todoItems'],
  components: {
    TodoItem
  },
  methods: {
    removeTodo(id: number) {
      this.$emit('remove-todo', id)
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
