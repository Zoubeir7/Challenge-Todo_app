<template>
  <div class="app-container">
    <h1>Vue 3 Todo App</h1>
    <form @submit.prevent="addNewTodo" class="todo-form">
      <label>New Task</label>
      <input v-model="newTodo" name="newTodo" class="todo-input">
      <button class="add-button">Add</button>
    </form>
    <h2>{{ newTodo }}</h2>
    <div class="controls">
      <button @click="markAllDone" class="control-button">Mark All Done</button>
      <button @click="removeAll" class="control-button">Remove All</button>
    </div>
    <ul class="todo-list">
      <li v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
        <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">{{ todo.content }}</h3>
        <button @click="removeTodo(index)" class="remove-button">Remove Task</button>
      </li>
    </ul>
  </div>
</template>
<script>
import { ref } from "vue";

export default {
  setup() {
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = '';
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach((todo) => (todo.done = true));
    }

    function removeAll() {
      todos.value.length = 0;
    }

    return {
      removeTodo,
      toggleDone,
      todos,
      newTodo,
      addNewTodo,
      markAllDone,
      removeAll,
    };
  },
};
</script>
<style scoped>
.app-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 2rem;
  background: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  color: #333;
}

.todo-form {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

.todo-input {
  flex: 1;
  padding: 0.5rem;
  margin-right: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.add-button {
  padding: 0.5rem 1rem;
  background: #28a745;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.add-button:hover {
  background: #218838;
}

.controls {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}

.control-button {
  padding: 0.5rem 1rem;
  background: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.control-button:hover {
  background: #0056b3;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem;
  border-bottom: 1px solid #ccc;
}

.todo-item h3 {
  margin: 0;
  cursor: pointer;
}

.todo-item h3.done {
  text-decoration: line-through;
  color: #999;
}

.remove-button {
  padding: 0.5rem;
  background: #dc3545;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.remove-button:hover {
  background: #c82333;
}
</style>
