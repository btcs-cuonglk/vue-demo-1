<template>
  <div id="app">
    <HeaderTop />
    <TodoView />
  </div>
</template>

<script>
import HeaderTop from './components/HeaderTop.vue'
import TodoView from './components/TodoView.vue'

export default {
  name: 'App',
  components: { HeaderTop, TodoView },
}
</script>

<style>
#app {
  font-family: Avenir, Arial, Helvetica, sans-serif;
}
</style>
