<script setup>
import { ref } from "vue";
import TaskList from './components/TaskList.vue'
const taskList = ref([]);
const inputTodo = ref('')
const addTodo = async () => {
  const todoForm = {
    id: Date.now(),
    name: inputTodo.value,
    isCompleted: false
  }
  taskList.value.push(todoForm)
  inputTodo.value = ''


}
const removeTodo = (id) => {
  const filteredTodo = taskList.value.filter(t => t.id !== id)
  taskList.value = filteredTodo;
}
const toggleIsCompleted = async (id) => {
  console.log(id);
  const updatedTask = taskList.value.map((task) => task.id === id ?
    { ...task, isCompleted: task.isCompleted = !task.isCompleted } : task)
  taskList.value = updatedTask
  console.log(updatedTask);
}

</script>
<template>
  <div>
    <h1 class="p-6 text-3xl font-bold text-center">Todo App 📋</h1>
    <div class="w-[360px] mx-auto p-3 ">
      <div class="flex items-center gap-2">
        <div class="relative  w-full min-w-[200px] h-10 ">
          <input v-model="inputTodo"
            class="peer w-full h-full bg-transparent text-blue-gray-700 font-sans font-normal outline outline-0 focus:outline-0 disabled:bg-blue-gray-50 disabled:border-0 transition-all placeholder-shown:border placeholder-shown:border-blue-gray-200 placeholder-shown:border-t-blue-gray-200 border focus:border-2 border-t-transparent focus:border-t-transparent text-sm px-3 py-2.5 rounded-[7px] border-blue-gray-200 focus:border-gray-900"
            placeholder="" /><label
            class="flex w-full h-full select-none pointer-events-none absolute left-0 font-normal !overflow-visible truncate peer-placeholder-shown:text-blue-gray-500 leading-tight peer-focus:leading-tight peer-disabled:text-transparent peer-disabled:peer-placeholder-shown:text-blue-gray-500 transition-all -top-1.5 peer-placeholder-shown:text-sm text-[11px] peer-focus:text-[11px] before:content[' '] before:block before:box-border before:w-2.5 before:h-1.5 before:mt-[6.5px] before:mr-1 peer-placeholder-shown:before:border-transparent before:rounded-tl-md before:border-t peer-focus:before:border-t-2 before:border-l peer-focus:before:border-l-2 before:pointer-events-none before:transition-all peer-disabled:before:border-transparent after:content[' '] after:block after:flex-grow after:box-border after:w-2.5 after:h-1.5 after:mt-[6.5px] after:ml-1 peer-placeholder-shown:after:border-transparent after:rounded-tr-md after:border-t peer-focus:after:border-t-2 after:border-r peer-focus:after:border-r-2 after:pointer-events-none after:transition-all peer-disabled:after:border-transparent peer-placeholder-shown:leading-[3.75] text-gray-500 peer-focus:text-gray-900 before:border-blue-gray-200 peer-focus:before:!border-gray-900 after:border-blue-gray-200 peer-focus:after:!border-gray-900">Input
            Todo
          </label>

        </div>
        <button v-on:click="addTodo"
          class="px-3 py-1 text-2xl font-bold bg-blue-600 rounded-full text-gray-50">+</button>
      </div>

      <section>
        <h2 class="p-6 text-3xl font-bold text-center">List of Todo</h2>
        <ul class="">
          <li v-for="task in taskList" :key="task.id" class="flex gap-3 p-2 my-2 rounded-sm shadow">
            <input type="checkbox" @change="toggleIsCompleted(task.id)">
            <p :class="{ ' line-through': task.isCompleted }">{{ task.name }} </p><button v-show="task.isCompleted"
              class="px-3 ml-auto bg-red-600 text-gray-50" @click="removeTodo(task.id)">Remove</button>
          </li>
        </ul>
      </section>
    </div>
  </div>
</template>