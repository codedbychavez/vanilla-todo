<template>
  <form @submit="handleFormSubmit" class="todo-form">
  <!-- TODO: Add form here -->
  </form>
</template>

<script>
import { v4 as uuid } from 'uuid';

export default {
  data() {
    return {
      id: '',
      title: '',
      isComplete: false,
    }
  },
  methods: {
    generateRandomId() {
      return uuid();
    },

    handleFormSubmit() {

    }
  }
}

</script>