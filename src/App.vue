<template>
  <main>
    <!-- Main stuff goes here -->
    <AppHeader />
    <!-- Add todo form -->
    <div class="todo-form-container">
      <TodoForm />
    </div>
    <div class="todos-container">
      <div class="todo-item-wrapper" v-for="todo of todos">
        <TodoItem
          :id="todo.id"
          :title="todo.title"
          :is-complete="todo.isComplete"
          @todo-status-change="handleTodoStatusChange"
        />
      </div>
    </div>
  </main>
</template>

<script>
import TodoItem from "./components/TodoItem.vue";
import AppHeader from "./components/AppHeader.vue";
import TodoForm from "./components/TodoForm.vue";
export default {
  components: {
    TodoItem,
    AppHeader,
    TodoForm,
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Some task thats needs to be done",
          isComplete: false,
        },
        {
          id: 2,
          title: "Some task thats needs to be done",
          isComplete: true,
        },
      ],
    };
  },
  methods: {
    updateTodo(status, index) {
      this.todos[index].isComplete = status;
    },

    handleTodoStatusChange(status, id) {
      // Filter the array to the individual todo item:
      let todoToUpdate = this.todos.filter((todo) => todo.id === id);

      // Find the idex of the todo
      let indexOfTodoToUpdate = this.todos.indexOf(todoToUpdate[0]);

      // Update the todo
      this.updateTodo(status, indexOfTodoToUpdate);
    },
  },
};
</script>

<style>

.todo-form-container {
  
}

.todos-container {
  @apply border p-4;
}

.todo-item-wrapper + .todo-item-wrapper {
  @apply mt-4;
}
</style>
