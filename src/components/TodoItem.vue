<template>
  <div class="todo-item">
    <div class="todo-status">
      <input type="checkbox" v-model="isChecked" @change="$emit('todoStatusChange', isChecked, id)" />
    </div>
    <div class="todo-title" :class="isComplete && 'strikethrough'">{{ title }}</div>
  </div>
</template>

<script>
export default {
  props: {
    id: Number,
    title: String,
    isComplete: Boolean,
  },
  data() {
    return {
      isChecked: this.isComplete,
    }
},
  methods: {
    handleCheckboxChange() {
      console.log('Checkbox changed ', this.isChecked);
    }
  }
}
</script>

<style>
.todo-item {
  @apply flex bg-slate-100 p-4 w-3/4 mx-auto;
}

.todo-status {
  @apply mr-4;
}

.strikethrough {
  @apply line-through;
}

</style>