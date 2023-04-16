<template>
  <form ref="todoForm" @submit.prevent="handleFormSubmit" class="todo-form">
    <div class="form-element">
      <input v-model="isComplete" type="checkbox" />
    </div>
    <div class="form-element">
      <input
        v-model="title"
        class="title-input"
        type="text"
        placeholder="title"
      />
    </div>
    <div class="form-element">
      <button class="submit-button" type="submit">Add</button>
    </div>
  </form>
</template>

<script>
import { v4 as uuid } from "uuid";

class Todo {
  constructor(id, title, isComplete) {
    this.id = id;
    this.title = title;
    this.isComplete = isComplete;
  }
}

export default {
  emits: ["addTodo"],
  data() {
    return {
      id: "",
      title: "",
      isComplete: false,
    };
  },
  methods: {
    generateRandomId() {
      return uuid();
    },

    handleFormSubmit() {
      this.id = this.generateRandomId();
      const todo = new Todo(this.id, this.title, this.isComplete);
      this.$emit("addTodo", todo);
      this.$refs.todoForm.reset();
    },
  },
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
