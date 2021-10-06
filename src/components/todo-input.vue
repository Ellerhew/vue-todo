<template>
  <div class="add">
    <input
      type="text"
      class="add_input"
      placeholder="Enter your task"
      v-model="newTodoItem"
      v-on:keyup.enter="addTodoItem"
    />
    <button class="add_button" v-on:click="addTodoItem">Add</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodoItem: "",
    };
  },
  methods: {
    addTodoItem() {
      if (this.newTodoItem == null) {
        return;
      }
      this.$emit("addItem", this.newTodoItem);
      this.newTodoItem = "";
    },
  },
};
</script>