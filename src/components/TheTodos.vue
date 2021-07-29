<template>
  <div class="cointainer"><new-todo></new-todo> <todo-list></todo-list></div>
</template>

<script>
import newTodo from "./newTodo.vue";
import todoList from "./todoList.vue";

export default {
  components: {
    newTodo,
    todoList,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    setHistory() {
      if (JSON.parse(localStorage.getItem("todoHistory")) != null) {
        const localTodos = JSON.parse(localStorage.getItem("todoHistory"));
        localTodos.forEach((todo) => this.todos.push(todo));
      }
    },
    saveData() {
      localStorage.setItem("todoHistory", JSON.stringify(this.todos));
    },
  },
  provide() {
    return {
      todos: this.todos,
      saveData: this.saveData,
    };
  },
  mounted() {
    this.setHistory();
  },
};
</script>