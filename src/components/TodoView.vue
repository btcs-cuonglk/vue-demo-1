<template>
  <AddTodo @add-item="addTodo" />
  <TodoItem
    v-for="todo in todos"
    :key="todo.id"
    :todoProps="todo"
    @item-completed="markCompleted"
    @delete-item="deleteTodo"
  />
</template>

<script>
import { ref } from 'vue'
import axios from 'axios'
import TodoItem from './TodoItem.vue'
import AddTodo from './AddTodo.vue'
export default {
  name: 'TodoView',
  components: { TodoItem, AddTodo },
  setup() {
    const todos = ref([])

    const getAllTodos = async () => {
      try {
        const res = await axios.get(
          'https://jsonplaceholder.typicode.com/todos?_limit=10'
        )
        todos.value = res.data
      } catch (error) {
        console.log(error)
      }
    }

    getAllTodos()

    const markCompleted = id => {
      todos.value = todos.value.map(todo => {
        if (todo.id === id) todo.completed = !todo.completed
        return todo
      })
    }

    const deleteTodo = async id => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        todos.value = todos.value.filter(todo => todo.id !== id)
      } catch (error) {
        console.log(error)
      }
    }

    const addTodo = async newTodo => {
      try {
        await axios.post('https://jsonplaceholder.typicode.com/todos/', newTodo)
        todos.value.push(newTodo)
      } catch (error) {
        console.log(error)
      }
    }

    return {
      todos,
      markCompleted,
      deleteTodo,
      addTodo,
    }
  },
}
</script>

<style></style>
