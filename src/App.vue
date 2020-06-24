<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <TodoList/>
  </div>
</template>

<script>
import TodoList from './components/todolist.vue';
export default {
  name: 'App',
  components: {
    
    TodoList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
 
}
</style>
