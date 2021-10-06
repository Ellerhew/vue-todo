<template>
  <ul class="list">
    <li
      class="list_item"
      v-for="(todoItem, index) in propsdata"
      :key="todoItem.key"
    >
      <input
        type="checkbox"
        :id="todoItem.key"
        :checked="todoItem.completed === true"
        v-on:change="toggleComplete(todoItem)"
      />
      <label :for="todoItem.key">
        <p class="list_content">{{ todoItem.item }}</p>
      </label>
      <button class="list_delete" v-on:click="removeTodo(todoItem, index)">
        Delete
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  props: ["propsdata"],
  methods: {
    removeTodo(todoItem) {
      this.$emit("removeItem", todoItem);
    },
    toggleComplete(todoItem) {
      this.$emit("toggleItem", todoItem);
    },
  },
};
</script>


<style>
.list {
  list-style: none;
}
.list_item {
  display: flex;
  align-items: center;
}
.list_item label {
  display: flex;
  align-items: center;
}
.list_title {
  margin: 0;
}
</style>
