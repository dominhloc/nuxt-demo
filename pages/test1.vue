<script setup>
import { ref, computed } from "vue";

const newTodo = ref("");
const hideCompleted = ref(false);
const todos = ref([
  { id: 1, text: "Công Việc 1", done: false, favorites: false },
  { id: 2, text: "Công Việc 2", done: false, favorites: false },
  { id: 3, text: "Công Việc 3", done: false, favorites: false },
  { id: 4, text: "Công Việc 4", done: false, favorites: false },
  { id: 5, text: "Công Việc 5", done: false, favorites: false },
]);

//mock API - hiển thị lên màn hình dữ liệu được trả về từ API
$fetch("https://6642ea4a3c01a059ea20c7c2.mockapi.io/NEWTODOLIST").then((x) => {
  todos.value = x;

  const countfalse = todos.value.filter((todo) => !todo.done).length;
  countFalseDisplay.textContent = countfalse;
});

function addTodo(todo) {
  // khai báo 1 mảng mới = độ dài mảng cũ + 1
  let newIndex = todos.value.length + 1;
  //console.log("🚀 ~ newIndex:", newIndex);

  // hàm push để nhập vào các giá trị mới
  todos.value.push({ id: newIndex, text: newTodo.value, done: false });
  // xóa input đầu vào , trả về rỗng
  newTodo.value = "";
}

function removeTodo(todo) {
  // dùng filter để lọc các phần tử có id trùng khớp

  // kiểm tra từng phần tử t của mảng todos.value.
  // Trả về true nếu id của phần tử hiện tại t khác với id của todo đang được loại bỏ
  // và false nếu ngược lại
  let x = todos.value.filter((t) => t.id !== todo.id);
  console.log("🚀 ~ todo.id:", todo.id);

  // cập nhật lại mảng gốc todos.value với kết quả đã lọc
  todos.value = x;
}

function gettodoClass(todo) {
  console.log("🚀 ~ gettodoClass ~ gettodoClass:", todo.done);
  ///
}

function favoritesTodo(todo) {
  todo.favorites = !todo.favorites;
  console.log("🚀 ~ todo.favorite:", todo.favorites);
}
</script>

<template>
  <div class="bg-slate-200 h-screen w-screen">
    <div class="bg-green-200 flex-col">
      <div
        class="text-6xl font-serif h-28 flex flex-row pl-4 justify-center items-center"
      >
        Todo List
      </div>
      <!-- nút enter để add -->
      <form
        class="flex justify-center font-serif items-center space-x-4 pb-3"
        @submit.prevent="addTodo"
      >
        <input
          class="bg-slate-300 h-16 w-1/3 rounded-2xl text-gray-800 pl-3"
          v-model="newTodo"
          required
          placeholder="Type here"
        />
        <button class="h-16 w-20 bg-slate-500 font-serif rounded-2xl">
          Add..
        </button>
      </form>
    </div>

    <div
      class="space-y-4 flex flex-col justify-center items-center p-20 pt-10 bg-slate-200 overflow-auto"
    >
      <div
        class="h-20 pl-3 bg-slate-400 font-bold flex justify-center overflow-auto items-center w-3/4 font-serif space-x-4 rounded-2xl text-xl"
        v-for="todo in todos"
        :key="todo.id"
      >
        <!-- {{ todo.done }} - nếu todo.done == true thì sẽ gạch ngang -->
        <span :class="todo.done ? 'line-through text-blue-600' : 'text-black'">
          {{ todo.text }}
        </span>
        <div class="flex flex-auto justify-end space-x-3 pr-4">
          <input
            class="w-5"
            type="checkbox"
            v-model="todo.done"
            @click="gettodoClass(todo)"
          />

          <button @click="favoritesTodo(todo)">
            <svg
              class="w-6"
              :class="todo.favorites ? 'text-red-500' : 'opacity-70 '"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
            >
              <path
                fill="currentColor"
                d="m12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5C2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3C19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54z"
              />
            </svg>
          </button>
          <button class="opacity-70" @click="removeTodo(todo)">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="1.2em"
              height="1.2em"
              viewBox="0 0 12 12"
            >
              <path
                fill="black"
                d="M5 3h2a1 1 0 0 0-2 0M4 3a2 2 0 1 1 4 0h2.5a.5.5 0 0 1 0 1h-.441l-.443 5.17A2 2 0 0 1 7.623 11H4.377a2 2 0 0 1-1.993-1.83L1.941 4H1.5a.5.5 0 0 1 0-1zm3.5 3a.5.5 0 0 0-1 0v2a.5.5 0 0 0 1 0zM5 5.5a.5.5 0 0 0-.5.5v2a.5.5 0 0 0 1 0V6a.5.5 0 0 0-.5-.5"
              />
            </svg>
          </button>
        </div>
      </div>
      <div class="flex flex-row justify-center space-x-2">
        <div>You have</div>
        <div class="font-bold text-red-500">{{ todos.length }}</div>
        <div>tasks left todo</div>
      </div>
    </div>
  </div>
</template>
