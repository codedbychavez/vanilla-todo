<template>
  <form ref="todoForm" @submit.prevent="handleFormSubmit()" class="todo-form">
    <div class="form-element">
      <input v-model="todo.status" type="checkbox" />
    </div>
    <div class="form-element">
      <input v-model="todo.title" class="title-input" type="text" placeholder="title" />
    </div>
    <div class="form-element">
      <button class="submit-button" type="submit">Add</button>
    </div>
  </form>
</template>

<script lang="ts" setup>
import { v4 as uuid } from "uuid";
import { Todo } from "../Models";
import { reactive } from "vue";

const emits = defineEmits(['addTodo']);

const todo: Todo = reactive({ id: "", title: "", status: false });

const generateRandomId = (): string => {
  return uuid();
};

const resetForm = (): void => {
  todo.id = "",
    todo.title = "",
    todo.status = false
}


const handleFormSubmit = () => {
  const generatedTodoId = generateRandomId();
  const todoToAdd: Todo = { id: generatedTodoId, title: todo.title, status: todo.status };
  emits('addTodo', todoToAdd)
  resetForm();
};


</script>

<style>
.todo-form {
  @apply flex gap-4 py-4 items-center justify-center;
}

.title-input {
  @apply border py-1 px-2 lg:w-96 w-full;
}

.submit-button {
  @apply px-6 py-1 bg-blue-500 text-white font-bold rounded !important;
}
</style>
