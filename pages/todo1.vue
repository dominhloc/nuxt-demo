<script setup>
import { ref, computed } from "vue";

const newtodo = ref("");
const hideCompleted = ref(false);
const todos = ref([
  // { id: 1, text: "Công Việc 1", done: false },
  // { id: 2, text: "Công Việc 2", done: false },
  // { id: 3, text: "Công Việc 3", done: false },
  // { id: 4, text: "Công Việc 4", done: false },
  // { id: 5, text: "Công Việc 5", done: false },
]);

//mock API - hiển thị lên màn hình dữ liệu được trả về từ API
$fetch("https://6642ea4a3c01a059ea20c7c2.mockapi.io/NEWTODOLIST").then((x) => {
  todos.value = x;
});
// dùng filter lọc các phần tử có giá trị là false rồi tính độ dài của chúng
function updateCountFalse() {
  const countfalse = todos.value.filter((todo) => !todo.done).length;
  const countFalseDisplay = document.getElementById("countFalseDisplay");
  countFalseDisplay.textContent = countfalse;
}

async function addTodo() {
  const res = await $fetch(
    "https://6642ea4a3c01a059ea20c7c2.mockapi.io/NEWTODOLIST",
    {
      method: "POST",
      body: { text: newtodo.value },
    }
  );
  newtodo.value = "";
  todos.value = await $fetch(
    "https://6642ea4a3c01a059ea20c7c2.mockapi.io/NEWTODOLIST"
  );
}
const filteredtodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});
//console.log("🚀 ~ filteredtodos ~ filteredtodos:", filteredtodos);

// function addTodo(todo) {
//   let newIndex = todos.value.length + 1;
//   todos.value.push({
//     id: newIndex,
//     text: newtodo.value,
//     done: false,
//     favorites: false,
//   });
//   newtodo.value = " ";
// }

async function removeTodo(todo) {
  let id = todo?.id;
  const res = await $fetch(
    `https://6642ea4a3c01a059ea20c7c2.mockapi.io/NEWTODOLIST/${id}`,
    {
      method: `DELETE`,
    }
  );
  todos.value = await $fetch(
    "https://6642ea4a3c01a059ea20c7c2.mockapi.io/NEWTODOLIST"
  );
}

// function removeTodo(todo) {
//   let x = todos.value.filter((t) => t.id !== todo.id);
//   //console.log("🚀 ~ todo.id:", todo.id); // id click vào
//   todos.jjkjjd = x;
// }

async function gettodoClass(todo) {
  //console.log("🚀 ~ gettodoClass :", todo.done);
  const res = await $fetch(
    `https://6642ea4a3c01a059ea20c7c2.mockapi.io/NEWTODOLIST/${todo?.id}`,
    {
      method: "PUT",
      body: todo,
    }
  );
}

const todos_old = ref([]);
let check_done = false;

function hideComp() {
  if (check_done === true) {
    todos.value = todos_old.value;
  } else {
    // Lưu trữ danh sách ban đầu vào todos_old
    todos_old.value = todos.value;

    // Tạo danh sách mới chỉ chứa các mục yêu thích
    const newList = todos.value.filter((todo) => todo.done === true);
    //console.log("🚀 ~ hideComp ~ newList:", newList);

    // Gán todos bằng danh sách mới
    todos.value = newList;
  }

  // Đảo ngược giá trị của biến check_done
  check_done = !check_done;
}
</script>

<template>
  <div
    class="flex flex-col justify-center items-center bg-gradient-to-l from-gray-800 via-gray-600 to-gray-800 h-screen w-screen"
  >
    <div class="container w-[450px] rounded-xl">
      <div class="p-6 space-y-5">
        <div class="font-serif text-6xl text-center text-white">Just do it</div>
        <div class="flex flex-row justify-center">
          <form @submit.prevent="addTodo">
            <input
              class="rounded-l-2xl p-2 w-52 font-serif bg-slate-500 text-white"
              v-model="newtodo"
              required
              placeholder="Add a task ...."
            />
            <button
              class="rounded-r-2xl font-serif p-2 bg-slate-400 text-white hover:bg-slate-500 duration-500"
            >
              I Got This
            </button>
          </form>
        </div>

        <div class="flex-col flex h-[300px] overflow-auto space-y-5 font-serif">
          <div
            class="flex flex-row rounded-full pl-1 border-y-2"
            v-for="todo in filteredtodos"
            :key="todo.id"
          >
            <div class="text-center p-2 text-yellow-400">{{ todo.id }} :</div>
            <!-- {{ todo.done }} -->
            <span
              class="flex flex-grow items-center"
              :class="todo.done ? 'line-through text-yellow-300' : 'text-white'"
            >
              {{ todo.text }}
            </span>

            <div class="flex space-x-2 justify-end">
              <div
                class="flex bg-slate-400 w-10 h-10 rounded-full justify-center hover:bg-slate-500 duration-500"
              >
                <input
                  type="checkbox"
                  class="w-5"
                  v-model="todo.done"
                  @change="gettodoClass(todo)"
                />
              </div>

              <button
                class="w-10 h-10 flex justify-center items-center bg-slate-400 hover:bg-slate-500 duration-500 rounded-full"
                @click="removeTodo(todo)"
              >
                <svg
                  class="h-8 w-9"
                  xmlns="http://www.w3.org/2000/svg"
                  width="1.2em"
                  height="1.2em"
                  viewBox="0 0 24 24"
                >
                  <path
                    fill="black"
                    d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V9c0-1.1-.9-2-2-2H8c-1.1 0-2 .9-2 2zM18 4h-2.5l-.71-.71c-.18-.18-.44-.29-.7-.29H9.91c-.26 0-.52.11-.7.29L8.5 4H6c-.55 0-1 .45-1 1s.45 1 1 1h12c.55 0 1-.45 1-1s-.45-1-1-1"
                  />
                </svg>
              </button>
            </div>
          </div>
        </div>
        <div class="flex flex-row justify-center">
          <div
            class="text-center font-serif text-white w-72 border-y-2 rounded-full hover:bg-slate-700 duration-500"
          >
            <div class="flex flex-row justify-center space-x-2">
              <div>You have</div>
              <p class="font-bold text-red-500" id="countFalseDisplay"></p>
              <div>/</div>
              <div class="font-bold text-red-500">{{ todos.length }}</div>
              <div>tasks left todo</div>
            </div>
          </div>
        </div>
        <div class="flex flex-row justify-center space-x-3">
          <button
            class="font-serif hover:bg-slate-700 duration-500 text-white border p-0 rounded-xl w-40 bg-gradient-to-l from-gray-800 via-gray-600 to-gray-800"
            @click="hideComp"
          >
            {{ "Show / Hide" }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
