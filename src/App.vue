<template>
  <div class="container">
    <h2>To-Do List</h2>
    <emit @add-btn="addlist"></emit>
    <div v-if="!todos.length">
      追加してください
    </div>
    <div 
      v-for="(todo, index) in todos"
      :key="todo.id"
      class="card mt-2"
    >
      <div class="card-body p-2 d-flex align-items-center">
        <div class="form-check flex-grow-1">
          <input 
            class="form-check-input" 
            type="checkbox"
            v-model="todo.completed"
          >
          <label 
            class="form-check-label"
            :class="{ todo: todo.completed }"
          >
            {{ todo.subject }}
          </label>
        </div>
        <div>
          <button 
            class="btn btn-danger btn-sm"
            @click="deleteTodo(index)"
          >
            Delete
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import emit from './components/emit.vue';

export default {
  components: { emit },
  
  setup() {
    const todo = ref('');
    const todos = ref([]);
    const hasError = ref(false);
    const addlist = (todo) => {
      todos.value.push(todo);
    }

    // const onSubmit = () => {
    //   if (todo.value === '') {
    //     hasError.value = true;
    //   } else {
    //     todos.value.push({
    //       id: Date.now(),
    //       subject: todo.value,
    //       completed: false,
    //     });
    //     hasError.value = false;
    //     todo.value = '';
    //   }
    // };

    const deleteTodo = (index) => {
      todos.value.splice(index, 1);
    };

    return {
      todo,
      todos,
      hasError,
      deleteTodo,
      addlist,
    };
  }
}
</script>

<style>
  .todo {
    color: gray;
    text-decoration: line-through;
  }
</style>