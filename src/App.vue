<template>
  <base-card>
    <header><h1>To Do List</h1></header>
    <todo-list list-name="Todo"></todo-list>
  </base-card>
</template>

<script>
import TodoList from "./components/TodoList.vue"
export default {
  name: "App",
  components: {
    TodoList,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
header {
  width: 100%;
  height: 5rem;
  background-color: #3a0061;
  display: flex;
  justify-content: center;
  align-items: center;
}

header h1 {
  color: white;
  margin: 0;
}
</style>
