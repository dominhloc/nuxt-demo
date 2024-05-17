<script setup>
import { ref, computed } from "vue";

const newtodo = ref("");
const hideCompleted = ref(false);
const todos = ref([
  { id: 1, text: "Công Việc 1", done: false, favorites: false },
  { id: 2, text: "Công Việc 2", done: false, favorites: false },
  { id: 3, text: "Công Việc 3", done: false, favorites: false },
  { id: 4, text: "Công Việc 4", done: false, favorites: false },
  { id: 5, text: "Công Việc 5", done: false, favorites: false },
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
  <div
    class="flex flex-col justify-center items-center bg-gray-800 h-screen w-screen"
  >
    <div
      class="container p-4 bg-blue-300 h-[500px] w-[450px] rounded-xl overflow-auto"
    >
      <div class="p-9 space-y-5">
        <div class="font-serif text-6xl text-center bg-slate-400 text-white">
          Just do it
        </div>

        <div class="flex flex-row justify-center">
          <form class="" @submit.prevent="addTodo">
            <input
              class="rounded-l-xl p-2 w-52 font-serif bg-slate-700 text-white"
              v-model="newtodo"
              required
              placeholder="Add a task ...."
            />
            <button class="rounded-r-xl font-serif p-2 bg-slate-400 text-white">
              I Got This
            </button>
          </form>
        </div>

        <div
          class="flex flex-col h-auto w-full px-2 space-y-5 font-serif bg-slate-500"
        >
          <div
            class="flex flex-col space-x-5 bg-slate-100 h-auto w-full px-2"
            v-for="todo in todos"
            :key="todo.id"
          >
            <div class="flex">
              <div class="bg-slate-300">
                <span :class="todo.done ? 'line-through' : 'text-black'">
                  {{ todo.text }}
                </span>
              </div>
              <div class="flex-auto text-end">
                <input
                  type="checkbox"
                  class=""
                  v-model="todo.done"
                  @change="gettodoClass(todo)"
                />
              </div>

              <!-- <button class="bg-red-500 w-5" @click="removeTodo(todo)">
                  X
                </button> -->
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
