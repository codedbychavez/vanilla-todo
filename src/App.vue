<template>

  <main>
    <!-- Main stuff goes here -->
    <AppHeader />
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
import TodoItem from './components/TodoItem.vue';
import AppHeader from './components/AppHeader.vue';
  export default {
    components: {
      TodoItem,
      AppHeader,
    },
    data() {
      return {
        todos: [
          {
            id: 1,
            title: 'Some task thats needs to be done',
            isComplete: false,
          },
          {
            id: 2,
            title: 'Some task thats needs to be done',
            isComplete: true,
          }
        ]
      }
    },
    methods: {
      handleTodoStatusChange(status, id) {
        console.log('Todo status change: ', status, id);
        // Actually use the params to update the data
      }
    }
  }
</script>


<style>

.todos-container {
  @apply border p-4;
}

.todo-item-wrapper + .todo-item-wrapper {
  @apply mt-4;
}

</style>
