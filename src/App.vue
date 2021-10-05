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
      todoItems: [],
    };
  },
  methods: {
    addOneItem(value) {
      const todoItem = {
        key: Date.now(),
        item: value,
        completed: false,
      };
      localStorage.setItem(todoItem.key, JSON.stringify(todoItem));
      this.todoItems.unshift(todoItem);
    },
    toggleOneItem(todoItem) {
      todoItem.completed = !todoItem.completed;
      localStorage.setItem(todoItem.key, JSON.stringify(todoItem));
    },
    removeOneItem(todoItem, index) {
      localStorage.removeItem(todoItem.key);
      this.todoItems.splice(index, 1);
    },
  },
  created() {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
          this.todoItems.push(
            JSON.parse(localStorage.getItem(localStorage.key(i)))
          );
        }
      }
    }
  },
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
