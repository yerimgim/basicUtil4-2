<template>
  <form @submit.prevent="submitTodo">
    <input type="text" v-model.trim="newTodoItem" v-on:keyup.enter="addTodo" />
    <span class="addContainer" v-on:click="addTodo">등록</span>
  </form>
</template>

<script>
export default {
  name: "CreateTodo",
  data() {
    return {
      newTodoItem: "",
    };
  },
  methods: {
    addTodo() {
      let todoItem = { item: this.newTodoItem, completed: false };
      if (todoItem !== "") {
        this.$emit("addTodo", todoItem);
        this.clearTodo();
      }
    },
    clearTodo() {
      this.newTodoItem = "";
    },
  },
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.addContainer {
  float: right;
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
</style>
