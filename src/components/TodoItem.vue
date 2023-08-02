<template>
  <div class="todo-item">
    <div class="todo-status">
      <input type="checkbox" v-model="props.todo.status" @change="handleTodoStatusChange()" />
    </div>
    <div class="todo-title" :class="props.todo.status && 'strikethrough'">
      {{ props.todo.title }}
    </div>
    <div class="delete-button-wrapper">
      <button @click="handleTodoDelete(props.todo.id)">
        <IconX />
      </button>
    </div>
  </div>
</template>

<script lang="ts" setup>

import { Todo } from '../Models';
import IconX from './IconX.vue';

const emits = defineEmits(['todoStatusChange', 'todoDelete']);

const props = defineProps<{
  todo: Todo
}>();

const handleTodoStatusChange = () => {
  const todo = props.todo;
  emits("todoStatusChange", todo.id, todo.status);
};

const handleTodoDelete = (id: string) => {
  emits("todoDelete", id);
};


</script>

<style>
.todo-item {
  @apply flex bg-slate-100 p-4 md:w-3/4 mx-auto;
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
