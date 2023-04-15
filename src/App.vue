<template>
  <main>
    <AppHeader />
    <div class="todo-form-container">
      <TodoForm @add-todo="handleAddTodo" />
    </div>
    <div class="todos-container">
      <div class="todo-item-wrapper" v-for="todo of todos">
        <TodoItem
          :todo="todo"
          @todo-status-change="handleTodoStatusChange"
          @todo-delete="handleTodoDelete"
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
          title: "This is task one",
          isComplete: false,
        },
        {
          id: 2,
          title: "This is task two",
          isComplete: true,
        },
      ],
    };
  },
  methods: {
    updateTodo(status, index) {
      this.todos[index].isComplete = status;
    },

    getIndexOfTodo(id) {
      const todoToLookFor = this.todos.filter((todo) => todo.id == id);
      return this.todos.indexOf(todoToLookFor[0]);
    },

    handleTodoStatusChange(id, status) {
      // Find the idex of the todo
      const indexOfTodoToUpdate = this.getIndexOfTodo(id);

      // Update the todo
      this.updateTodo(status, indexOfTodoToUpdate);
    },
    addTodo(todoToAdd) {
      this.todos.push(todoToAdd);
      console.log(this.todos);
    },
    handleAddTodo(todoToAdd) {
      this.addTodo(todoToAdd);
    },
    handleTodoDelete(id) {
      const indexOfTodoToDelete = this.getIndexOfTodo(id);
      this.todos.splice(indexOfTodoToDelete, 1);
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
