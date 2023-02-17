<template>
  <div class="container">
    <h1>todos</h1>
    <div class="wrap">
      <the-todos-form
        @mark-all-completed="markAllCompleted"
        @add-todo="addTodo"
      />
      <the-todos-list
        @delete-todo="deleteTodo"
        @toggle-status="toggleStatus"
        :todos="filterTodos"
      />
      <the-todos-footer
        @clear-completed-todos="clearCompletedTodos"
        @filter-todos="changeFilter"
        :itemsLeft="itemsLeft"
      />
    </div>
  </div>
</template>
<script>
import TheTodosFooter from "./components/TheTodosFooter.vue";
import TheTodosForm from "./components/TheTodosForm.vue";
import TheTodosList from "./components/TheTodosList.vue";

export default {
  data() {
    return {
      todos: [],
      filterType: "all",
    };
  },
  computed: {
    itemsLeft() {
      return this.todos.filter((todo) => todo.completed === false).length;
    },
    filterTodos() {
      if (this.filterType === "active") {
        return this.todos.filter((todo) => todo.completed === false);
      }
      if (this.filterType === "completed") {
        return this.todos.filter((todo) => todo.completed === true);
      }
      return this.todos;
    },
  },
  methods: {
    addTodo(todo) {
      this.todos.push(todo);
    },
    deleteTodo(idx) {
      this.todos.splice(idx, 1);
    },
    changeFilter(filterType) {
      this.filterType = filterType;
    },
    toggleStatus(idx) {
      this.todos[idx].completed = !this.todos[idx].completed;
    },
    clearCompletedTodos() {
      this.todos = this.todos.filter((todo) => todo.completed !== true);
    },
    markAllCompleted() {
      this.todos.forEach((todo) => (todo.completed = true));
    },
  },
  components: {
    TheTodosFooter,
    TheTodosForm,
    TheTodosList,
  },
};
</script>
<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0 auto;
  width: 550px;
}
.wrap {
  width: 100%;
  box-shadow: 0 2px 4px 0 rgb(0 0 0 / 20%), 0 25px 50px 0 rgb(0 0 0 / 10%);
}
h1 {
  font-size: 100px;
  margin: 0;
}
</style>
