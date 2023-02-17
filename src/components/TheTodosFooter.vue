<template>
  <div>
    <p v-if="itemsRemain > 0">{{ itemsRemain }} items left</p>
    <select v-model="filterType" @change="handleChange(filterType)">
      <option value="all">All</option>
      <option value="active">Active</option>
      <option value="completed">Completed</option>
    </select>
    <button @click="handleClearCompleted">Clear completed</button>
  </div>
</template>
<script>
export default {
  name: "TheTodosFoote",
  props: {
    itemsLeft: {
      type: Number,
      required: true,
    },
  },
  computed: {
    itemsRemain() {
      return this.itemsLeft;
    },
  },
  data() {
    return {
      filterType: "all",
    };
  },
  methods: {
    handleChange(value) {
      this.$emit("filterTodos", value);
    },
    handleClearCompleted() {
      this.$emit("clearCompletedTodos");
    },
  },
};
</script>
<style lang=""></style>
