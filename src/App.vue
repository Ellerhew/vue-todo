<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addItem="addOneItem"></TodoInput>
    <TodoList
      :propsdata="todoItems"
      v-on:removeItem="removeOneItem"
      v-on:toggleItem="toggleOneItem"
    ></TodoList>
  </div>
</template>

<script>
import TodoHeader from "./components/todo-header.vue";
import TodoInput from "./components/todo-input.vue";
import TodoList from "./components/todo-list.vue";

export default {
  data() {
    return {
      todoItems: this.loadTodos() || [
        { key: 1, item: "haha", completed: false },
      ],
    };
  },
  methods: {
    addOneItem(value) {
      const todoItem = {
        key: Date.now(),
        item: value,
        completed: false,
      };
      this.todoItems.unshift(todoItem);
      localStorage.setItem("TODOS", JSON.stringify(this.todoItems));
    },
    toggleOneItem(todoItem) {
      todoItem.completed = !todoItem.completed;
      localStorage.setItem("TODOS", JSON.stringify(this.todoItems));
    },
    removeOneItem(item) {
      console.log(this.todoItems);
      const updated = this.todoItems.filter(
        (todoItem) => todoItem.key !== item.key
      );
      console.log(updated);
      this.todoItems = updated;
      localStorage.setItem("TODOS", JSON.stringify(updated));
    },
    loadTodos() {
      const toDos_ls = localStorage.getItem("TODOS");
      if (toDos_ls === null) {
        return;
      }
      const toDos = JSON.parse(toDos_ls);
      console.log(toDos);
      return toDos;
    },
  },
  // created() {
  //   this.todoItems = JSON.parse(localStorage.getItem("TODOS"));
  // },

  components: {
    TodoHeader,
    TodoInput,
    TodoList,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: rgb(136, 148, 187);
  width: 650px;
  margin: 100px auto;
}
</style>
