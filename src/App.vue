<template>
  <div class="flex h-screen w-screen bg-orange-300 justify-center p-10">
    <div class="flex h-full w-1/3 bg-white rounded-lg drop-shadow-xl p-4">
      <div class="w-full h-full flex flex-col gap-2">
        <div class="w-full h-auto flex justify-center pb-8">
          <h1 class="font-bold text-2xl text-gray-600">Todo App</h1>
        </div>
        
        <div class="w-full h-12 bg-white flex flex-row gap-2">
          <input class="flex-1 border-gray-300 rounded focus:border-orange-500 focus:ring-orange-500" type="text" v-model="newTodo">
          <button class="flex-non w-auto  bg-orange-500 text-white px-6 rounded" @click.prevent="AddTodo">Add</button>
        </div>
        <div class="w-full h-full bg-orange-100 p-2 rounded ">
          <div class="h-14 w-full bg-white rounded flex flex-row items-center gap-4 p-2 mb-2"  v-for="(todo, index) in todos" :key="todo.id">
            <div class="h-full w-4 rounded" :class="{done : todo.done, notDone : !todo.done }"></div>
            <input type="checkbox"  class="rounded border-gray-300 focus:ring-green-400 text-green-500" v-model="todo.done">
            <h2 class="flex-1 font-medium text-lg" :class="{doneTodo : todo.done}">{{todo.content}}</h2>
            <button class="flex-non h-full w-auto bg-red-500 text-white px-6 rounded" @click="deleteTodo(index)">Delete</button>
          </div>
        </div>
      </div>
    </div>  
  </div>
</template>

<script setup>
import {ref} from 'vue'

const newTodo = ref('')
const todos = ref([])
function AddTodo () {
  if(newTodo.value != ''){
     todos.value.push({
    id : todos.value.length + 1,
    content : newTodo.value,
    done : false
  })
  newTodo.value = ''
  }
 
}

function deleteTodo (index){
  todos.value.splice(index, 1)
}
</script>

<style>
.done {
  background-color: #22c55e;
  
}
.doneTodo {
  text-decoration: line-through;
  color : #525252
}
.notDone {
  background-color: #f97316;
}
</style>
