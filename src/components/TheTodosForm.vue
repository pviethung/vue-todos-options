<template>
  <div
    :style="{
      display: 'flex',
    }"
  >
    <button @click="markAllCompleted">Mark all completed</button>
    <form @submit.prevent="submit">
      <input v-model="todo" placeholder="What need to be done" type="text" />
    </form>
  </div>
</template>
<script>
export default {
  name: "TheTodosForm",
  data() {
    return {
      todo: "",
    };
  },
  methods: {
    markAllCompleted() {
      this.$emit("markAllCompleted");
    },
    submit() {
      this.$emit("addTodo", {
        name: this.todo,
        completed: false,
      });
      this.todo = "";
    },
  },
};
</script>
<style scoped>
form {
  width: 100%;
}
input {
  width: 100%;
  padding: 16px 16px 16px 60px;
  border: none;
  background: #fff;
  font-size: 24px;
  box-shadow: inset 0 -2px 1px rgb(0 0 0 / 3%);
  outline: none;
}
</style>
