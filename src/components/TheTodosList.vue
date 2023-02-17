<template>
  <ul>
    <li v-for="(todo, idx) in todos" :key="todo">
      <input
        @change="handleChange(idx)"
        type="checkbox"
        :checked="todo.completed"
      />
      <label>{{ todo.name }}</label>
      <button @click="handleDelete(idx)">Delele</button>
    </li>
  </ul>
</template>
<script>
export default {
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
  methods: {
    handleChange(todoIdx) {
      this.$emit("toggleStatus", todoIdx);
    },
    handleDelete(todoIdx) {
      this.$emit("deleteTodo", todoIdx);
    },
  },
};
</script>
<style scoped>
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
li {
  display: flex;
  align-items: center;
}
input {
  height: 40px;
  border-radius: 50%;
  text-align: center;
}
label {
  padding: 15px 15px 15px 60px;
  width: 100%;
  border-bottom: 1px solid #ededed;
}
</style>
