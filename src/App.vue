<template>
  <div id="app">
    <div class="container">
      <TodoHeader></TodoHeader>
      <TodoInput v-on:addItem="addOneItem"></TodoInput>
      <TodoList
        :propsdata="todoItems"
        v-on:removeItem="removeOneItem"
        v-on:toggleItem="toggleOneItem"
      ></TodoList>
    </div>
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
      const updated = this.todoItems.filter(
        (todoItem) => todoItem.key !== item.key
      );
      this.todoItems = updated;
      localStorage.setItem("TODOS", JSON.stringify(updated));
    },
    loadTodos() {
      const toDos_ls = localStorage.getItem("TODOS");
      if (toDos_ls === null) {
        return;
      }
      const toDos = JSON.parse(toDos_ls);
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
* {
  box-sizing: border-box;
}
#app {
  width: 100vw;
  height: 100vh;
  background-color: rgb(50, 66, 61);
  display: flex;
  align-items: center;
}
.container {
  background-color: rgb(237, 241, 238);
  width: 800px;
  height: 600px;
  margin: auto;
  border-radius: 10px;
  box-shadow: 0px 5px 13px 5px #90a191;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px 30px;
}
</style>
