<template>
  <form @submit.prevent="handleFormSubmit" class="todo-form">
    <div class="form-element">
      <input v-model="formData.isComplete" type="checkbox" />
    </div>
    <div class="form-element">
      <input v-model="formData.title" class="title-input" type="text" placeholder="title" />
    </div>
    <div class="form-element">
      <button class="submit-button" type="submit">Add</button>
    </div>
  </form>
</template>

<script>
import { v4 as uuid } from 'uuid';

export default {
  data() {
    return {
      formData: {
        id: '',
        title: '',
        isComplete: false,
      }
    }
  },
  methods: {
    generateRandomId() {
      return uuid();
    },

    handleFormSubmit() {
      this.formData.id = this.generateRandomId();
      console.log(this.formData);
    }
  }
}

</script>

<style>
.todo-form {
  @apply flex gap-4 py-4 items-center w-max mx-auto;
}

.title-input {
  @apply border py-1 px-2 w-96;
}

.submit-button {
  @apply px-6 py-1 bg-blue-500 text-white font-bold rounded !important;
}
</style>