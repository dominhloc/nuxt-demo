<script setup>
import { ref, computed } from "vue";

const newtodo = ref("");
const hideCompleted = ref(false);
const todos = ref([
  { id: 1, text: "Công Việc 1", done: false, favorites: false },
  { id: 2, text: "Công Việc 2", done: false, favorites: false },
  { id: 3, text: "Công Việc 3", done: false, favorites: false },
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

function removeTodo(todo) {
  let x = todos.value.filter((t) => t.id !== todo.id);
  console.log("🚀 ~ todo.id:", todo.id); // id click vào

  todos.value = x;
}

function gettodoClass(todo) {
  console.log("🚀 ~ gettodoClass:", todo);
  if (todo.done) {
    return "line-through";
  } else {
    return "text-white";
  }
}
</script>

<template>
  <div class="flex flex-col justify-center items-center bg-gray-800 h-screen">
    <div class="p-9 space-y-5">
      <div class="font-serif text-6xl text-center text-white">Just do it</div>
      <div class="flex flex-row">
        <form class="" @submit.prevent="addTodo">
          <input
            class="rounded-l-xl p-2 w-52 bg-slate-700 text-white"
            v-model="newtodo"
            required
            placeholder="Add a task ...."
          />
        </form>
        <button class="rounded-r-xl font-serif w-24 bg-slate-400 text-white">
          I Got This
        </button>
      </div>

      <li v-for="todo in todos" :key="todo.id">
        <span :class="todo.done ? 'line-through text-blue-600' : 'text-black'">
          {{ todo.text }}
        </span>
        <input
          type="checkbox"
          v-model="todo.done"
          @change="gettodoClass(todo)"
        />

        <button class="" @click="removeTodo(todo)">x</button>
      </li>
    </div>
  </div>
  <div></div>
</template>
