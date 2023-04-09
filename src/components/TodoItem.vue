<template>
  <div class="todo-item">
    <div class="todo-status">
      <input
        type="checkbox"
        v-model="isTodoComplete"
        @change="handleTodoStatusChange(todo)"
      />
    </div>
    <div class="todo-title" :class="isTodoComplete && 'strikethrough'">
      {{ todo.title }}
    </div>
    <div class="delete-button-wrapper">
      <button @click="handleTodoDelete(todo.id)">X</button>
    </div>
  </div>
</template>

<script>
export default {
  emits: ["todoStatusChange", "todoDelete"],
  props: {
    todo: Object,
  },
  data() {
    return {
      isTodoComplete: this.todo.isComplete,
    };
  },
  methods: {
    handleTodoStatusChange() {
      this.$emit("todoStatusChange", this.todo.id, this.isTodoComplete);
    },
    handleTodoDelete(id) {
      this.$emit("todoDelete", id);
    },
  },
};
</script>

<style>
.todo-item {
  @apply flex bg-slate-100 p-4 w-3/4 mx-auto;
}

.todo-status {
  @apply mr-4;
}

.delete-button-wrapper {
  @apply ml-auto;
}

.strikethrough {
  @apply line-through;
}
</style>
