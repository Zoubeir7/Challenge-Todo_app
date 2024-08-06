<template>
<div><h1>Vue 3 Todo App</h1>
  <form @submit.prevent ="addNewTodo"> <label>New Task </label>
    <input v-model="newTodo" name="newTodo">
    <button>Add</button>
    <h2>{{newTodo}}</h2>
  </form>
  <button @click="markAllDone">MarkALDone</button>
  <button @click="removeAll">RemoveAll</button>
  <ul><li v-for="(todo,index) in todos" key="todo.id" class="todo">
    <h3 :class="{ done:todo.done}" @click="toggleDone(todo)">{{todo.content}}</h3>
    <button @click="removeTodo(index)">Remove Task</button>
  </li></ul></div>
</template>

<script>
import  { ref } from "vue";

export default {
  setup(){
    const  newTodo =ref('');
    const  todos =ref([])
//add task
    function  addNewTodo(){
    todos.value.push({
      id:Date.now(),
      done:false,
      content: newTodo.value,
    })
      newTodo.value=''
    }
//barer les task
    function toggleDone(todo){
      todo.done =!todo.done;
    }

//delete task
function  removeTodo(index){
      todos.value.splice(index,1)
}
function  markAllDone(){
      todos.value.forEach((todo)=>todo.done=true);
}
function removeAll(){
 todos.value.length=0
}

    return {
      removeTodo,
      toggleDone,
      todos,
      newTodo,
      addNewTodo,
      markAllDone,
      removeAll,
    }
  }

}</script>


<style scoped>
.todo {
  cursor:pointer;
}
.done{
  text-decoration: line-through}

div{
  flex-direction: column;
  height: 100px;
}


</style>
