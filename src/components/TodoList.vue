<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in todo" v-bind:key="index">
        <i class="fas fa-check checkBtn" @click="toggleComplete(index)"></i>
        <span
          :style="todoItem.completed ? 'text-decoration: line-through' : ''"
        >
          {{ todoItem.item }}
        </span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  props: ["todo"],
  methods: {
    toggleComplete(index) {
      this.$emit("updateTodo", index);
    },
    removeTodo(todoItem, index) {
      this.$emit("removeTodo", todoItem, index);
    },
  },
};
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  align-items: center;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.checkBtn {
  display: flex;
}
.removeBtn {
  margin-left: auto;
}
</style>
