<template>
  <main>
    <AppHeader />
    <div class="todo-form-container">
      <TodoForm @add-todo="handleAddTodo" />
    </div>
    <div class="todos-container">
      <div class="todo-item-wrapper" v-for="todo of state.todos">
        <TodoItem :todo="todo" @todo-status-change="handleTodoStatusChange" @todo-delete="handleTodoDelete" />
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
import TodoItem from "./components/TodoItem.vue";
import AppHeader from "./components/AppHeader.vue";
import TodoForm from "./components/TodoForm.vue";
import { reactive } from "vue";
import { Todo } from './Models'

const state = reactive({
  todos: [] as Todo[],
});

const updateTodo = (status: boolean, index: number) => {
  state.todos[index].status = status;
};

const getIndexOfTodo = (id: string) => {
  const todoIndex = state.todos.findIndex((todo: Todo) => todo.id == id);
  return todoIndex;
};


const handleTodoStatusChange = (id: string, status: boolean) => {
  // Find the idex of the todo
  const indexOfTodoToUpdate = getIndexOfTodo(id);

  // Update the todo
  updateTodo(status, indexOfTodoToUpdate);
};

const addTodo = (todoToAdd: Todo) => {
  state.todos.push(todoToAdd);
};

const handleAddTodo = (todoToAdd: Todo) => {
  addTodo(todoToAdd);
};

const handleTodoDelete = (id: string) => {
  const indexOfTodoToDelete = getIndexOfTodo(id);
  state.todos.splice(indexOfTodoToDelete, 1);
};

</script>

<style>
.todos-container {
  @apply p-4;
}

.todo-item-wrapper+.todo-item-wrapper {
  @apply mt-4;
}
</style>
