<template>
    <form @submit.prevent="onSubmit">
        <input type="text" v-model="title" />
        <button type="submit">Create</button>
    </form>
</template>

<script lang="ts">
export default {
    methods: {
        onSubmit() {
            if (!this.title) return;

            const newTodo = {
                id: Date.now(),
                title: this.title,
                completed: false,
            }

            this.$emit('add-todo', newTodo)
            this.title = ''
        }
    },
    data() {
        return {
            title: ''
        }
    }
}
</script>

<style scoped>
form {
    display: flex;


}

input {
    width: 400px;
    margin-right: 20px;
}
</style>