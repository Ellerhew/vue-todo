<template>
  <ul class="list">
    <li
      class="list_item"
      :class="todoItem.completed ? 'complete' : ''"
      v-for="(todoItem, index) in propsdata"
      :key="todoItem.key"
    >
      <label :for="todoItem.key">
        <p class="list_content">{{ todoItem.item }}</p>
        <i class="fas fa-check"></i>
      </label>
      <input
        class="list_checkbox"
        type="checkbox"
        :id="todoItem.key"
        :checked="todoItem.completed === true"
        v-on:change="toggleComplete(todoItem)"
      />
      <button class="list_delete" v-on:click="removeTodo(todoItem, index)">
        <i class="far fa-trash-alt"></i>
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
  padding: 0px;
  margin: 0px;
  width: 100%;
}
.list_item {
  display: flex;
  align-items: center;
  padding: 0px 15px;
  border-radius: 20px;
  margin-bottom: 10px;
}
.list_item label {
  display: flex;
  align-items: center;
  flex: 1;
  justify-content: space-between;
  cursor: pointer;
  margin-right: 10px;
}
.list_item:hover {
  background-color: rgba(36, 35, 35, 0.075);
}
/* .list_item label:hover .fas.fa-check {
  color: #6e806f;
} */
.list_checkbox {
  display: none;
}
.list_title {
  margin: 0;
}
.list_content {
  flex: 1;
  color: #6e806f;
}
.fas.fa-check {
  width: 25px;
  font-size: 20px;
  text-align: center;
  color: #a9c7ab;
}
.fas.fa-check:hover {
  color: #6e806f;
}
.list_item.complete {
  background-color: rgba(36, 35, 35, 0.075);
}
.list_item.complete .list_content {
  text-decoration-line: line-through;
}
.list_item.complete .fas.fa-check {
  color: #6e806f;
}
/* .list_item.incomplete .fas.fa-check {
  color: #a9c7ab;
  color: #6e806f;
} */
.list_delete {
  cursor: pointer;
  background-color: transparent;
  outline: none;
  border: none;
}
.list_delete:hover .far.fa-trash-alt {
  color: #6e806f;
}
.far.fa-trash-alt {
  color: #a9c7ab;
  font-size: 20px;
}
</style>
