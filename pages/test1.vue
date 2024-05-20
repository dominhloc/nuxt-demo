<script setup>
import { ref, computed } from "vue";

const newtodo = ref("");
const hideCompleted = ref(false);
const todos = ref([
  { id: 1, text: "Công Việc 1", done: false },
  { id: 2, text: "Công Việc 2", done: false },
  { id: 3, text: "Công Việc 3", done: false },
  { id: 4, text: "Công Việc 4", done: false },
]);
function addTodo(todo) {
  let newIndex = todos.value.length + 1;
  todos.value.push({
    id: newIndex,
    text: newtodo.value,
    done: false,
    favorites: false,
  });
  newtodo.value = " ";
}
</script>

<template>
  <div class="flex items-center justify-center min-h-screen bg-gray-100">
    <div class="relative w-72 h-72 bg-blue-500 rounded-full">
      <div
        class="absolute top-0 left-0 w-1/2 h-1/2 bg-blue-500 rounded-tl-full"
      ></div>
      <div
        class="absolute top-0 right-0 w-1/2 h-1/2 bg-red-500 rounded-tr-full"
      ></div>
      <div
        class="absolute bottom-0 left-0 w-1/2 h-1/2 bg-green-500 rounded-bl-full"
      ></div>
      <div
        class="absolute bottom-0 right-0 w-1/2 h-1/2 bg-yellow-500 rounded-br-full"
      ></div>
      <div
        class=".slice:nth-child(1) { transform: rotate(0deg);} 'bg-red-500'"
        v-for="todo in todos"
        :key="todo.id"
      >
        {{ todo.text }}
      </div>
    </div>
  </div>
</template>
