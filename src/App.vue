<template>
  <h1>Todo list</h1>
  <TodoList
    :todo="todoItems"
    @updateTodo="updateTodo"
    @removeTodo="removeTodo"
  />
  <CreateTodo @addTodo="addTodo" />
</template>

<script>
import CreateTodo from "./components/CreateTodo.vue";
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  components: {
    CreateTodo,
    TodoList,
  },
  data() {
    return { todoItems: [] };
  },
  methods: {
    addTodo(todoItem) {
      this.todoItems.push(todoItem);
    },
    updateTodo(index) {
      this.todoItems[index].completed = !this.todoItems[index].completed;
    },
    removeTodo(todoItem, index) {
      this.todoItems.splice(index, 1);
      localStorage.removeItem(todoItem.item);
    },
  },
  created() {
    for (let i = 0; i < localStorage.length; i++) {
      const key = localStorage.key(i);
      try {
        const value = JSON.parse(localStorage.getItem(key));
        this.todoItems.push(value);
      } catch (e) {
        console.error("error", e);
      }
    }
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
body {
  display: flex;
  justify-content: center;
}
</style>
