<template>
  <div class="add">
    <input
      type="text"
      class="add_input"
      placeholder="Enter your task"
      v-model="newTodoItem"
      v-on:keyup.enter="addTodoItem"
    />
    <button class="add_button" v-on:click="addTodoItem">
      <i class="fas fa-plus"></i>
    </button>
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

<style>
.add {
  width: 100%;
  /* height: 50px; */
  display: flex;
  margin: 20px 0px;
  border-bottom: 2px solid #6e806f;
  padding: 10px;
}
.add_input {
  flex: 1;
  background-color: transparent;
  outline: none;
  border: none;
  color: #6e806f;
  font-size: 25px;
}
.add_button {
  background-color: #6e806f;
  border: none;
  outline: none;
  border-radius: 50%;
  width: 35px;
  height: 35px;
  cursor: pointer;
}
.add_button:hover {
  background-color: #a9c7ab;
}
.add_button:hover i {
  color: #6e806f;
}
.add_button i {
  font-size: 1.2rem;
  color: rgb(237, 241, 238);
}
</style>