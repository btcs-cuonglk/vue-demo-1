<template>
  <form @submit="addItem">
    <input type="text" placeholder="Nhập việc mới..." v-model="title" />
    <input type="submit" name="Thêm" class="btn-add" />
  </form>
</template>

<script>
import { ref } from 'vue'
export default {
  name: 'AddTodo',
  setup(props, context) {
    const title = ref('')
    const addItem = event => {
      event.preventDefault()

      const newItem = {
        title: title.value,
        completed: false,
      }

      context.emit('add-item', newItem)
      title.value = ''
    }
    return {
      title,
      addItem,
    }
  },
}
</script>

<style scoped>
form {
  display: flex;
}
input[type='text'] {
  flex: 10;
}
input[type='submit'] {
  flex: 2;
}
</style>
