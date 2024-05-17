<script setup>
import { ref, computed } from "vue";

const newtodo = ref("");
const hideCompleted = ref(false);
const todos = ref([
  // { id: 1, text: "Công Việc 1", done: false, favorites: false },
  // { id: 2, text: "Công Việc 2", done: false, favorites: false },
  // { id: 3, text: "Công Việc 3", done: false, favorites: false },
  // { id: 4, text: "Công Việc 4", done: false, favorites: false },
]);

const todos_old = ref([]); // giữ lại giá trị mảng cũ
let check_favorite = false; // khai báo biến check favorite = false

// hiển thị lên màn hình dữ liệu được trả về từ API
// const dataTwice = await $fetch(
//   "https://6642ea4a3c01a059ea20c7c2.mockapi.io/TODOLIST"
// );

$fetch("https://6642ea4a3c01a059ea20c7c2.mockapi.io/TODOLIST").then((x) => {
  todos.value = x;
  //console.log("🚀 ~ $fetch ~ x:", x);

  // khai báo arrLength để đo độ dài
  // let arrayLength = todos.value.length;
  // console.log("🚀 ~ $fetch ~ arrayLength:", arrayLength);

  // Sử dụng filter để lọc các giá trị true và đếm số lượng phần tử còn lại
  const countfalse = todos.value.filter((todo) => !todo.done).length;
  console.log("🚀 ~ $fetch ~ countfalse:", countfalse);

  const countFalseDisplay = document.getElementById("countFalseDisplay");

  countFalseDisplay.textContent = countfalse;

  // sắp xếp ngẫu nhiên các tasks
  // for (let i = arrayLength - 1; i > 0; i--) {
  //   let j = Math.floor(Math.random() * (i + 1));
  //   let k = x[i];
  //   x[i] = x[j];
  //   x[j] = k;
  // }
  // console.log("🚀 ~ points:", x);
});

// function addtodo() {
//   let newIndex = todos.value.length + 1;
//   todos.value.push({
//     id: newIndex,
//     text: newtodo.value,
//     done: false,
//     favorites: false,
//   });
//   //console.log(todos.value);
//   //xóa input đầu vào
//   newtodo.value = "";

//code tính năng update dùng hàm POSH
async function contactForm() {
  const res = await $fetch(
    "https://6642ea4a3c01a059ea20c7c2.mockapi.io/TODOLIST",
    {
      method: "POST",
      body: { text: newtodo.value },
    }
  );
  newtodo.value = "";
  todos.value = await $fetch(
    "https://6642ea4a3c01a059ea20c7c2.mockapi.io/TODOLIST"
  );
}
//lọc các giá trị mới được thêm vào
const filteredtodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});

// function removeTodo(todo) {
//   //console.log("🚀 ~ todo:", todo);
//   let x = todos.value.filter((t) => t.id !== todo.id); //todo.id = giá trị của id
//   //console.log("🚀 ~ todo.id:", todo.id);
//   todos.value = x;
//   console.log("🚀 ~ todos.value:", todos.value);
// }

async function removeTodo(todo) {
  let id = todo?.id;
  console.log("🚀 ~ id:", id);
  const res = await $fetch(
    `https://6642ea4a3c01a059ea20c7c2.mockapi.io/TODOLIST/${id}`,
    {
      method: "DELETE",
    }
  );
  todos.value = await $fetch(
    "https://6642ea4a3c01a059ea20c7c2.mockapi.io/TODOLIST" // đặt lại mảng ban đầu
  );
  //console.log(res);
}

// function gettodoClass(todo) {
//   // todo ở đây là param
//   if (todo.done) {
//     //console.log("🚀 ~ gettodoClass ~ todo.done:", todo.done);
//     return "line-through text-blue-600";
//   }
// }

async function gettodoClass(item) {
  // dùng item để k bị lỗi trùng lặp quá nhiều
  //console.log("🚀 ~ item:", item); // done sẽ từ false chuyển sang true
  const res = await $fetch(
    `https://6642ea4a3c01a059ea20c7c2.mockapi.io/TODOLIST/${item?.id}`,
    {
      method: "PUT",
      body: item,
      headers: {
        "Content-Type": "application/json",
      },
    }
  );
}

async function favoritesTodo(todo) {
  todo.favorites = !todo.favorites; // phương thức đảo ngược
  const res = await $fetch(
    `https://6642ea4a3c01a059ea20c7c2.mockapi.io/TODOLIST/${todo?.id}`,
    {
      method: "PUT",
      body: todo,
      headers: {
        "Content-Type": "application/json",
      },
    }
  );
}


//lọc ra các thành phần có fav = true và trả về mảng ban đầu
//tạo function mới có chức năng hiện ra những công việc yêu thích
function showFavorites() {
  const list_todo = ref([]);
  if (check_favorite == true) {
    todos.value = todos_old.value;
    //
    check_favorite = false;
  } else {
    // case mặc định
    todos_old.value = todos.value;
    for (let i = 0; i < todos.value.length; i++) {
      if (todos.value[i].favorites == true) {
        list_todo.value.push(todos.value[i]);
      }
    }
    todos.value = list_todo.value;
    check_favorite = true;
  }
}
</script>

<template>
  <div class="bg-cyan-500 h-screen flex flex-col justify-center items-center">
    <div
      class="container mx-auto p-4 flex flex-col bg-white h-[600px] w-[450px] space-y-3 rounded-xl justify-between"
    >
      <h1
        class="text-3xl text-center font-bold font-serif hover:bg-gray-300 duration-500"
      >
        Todo App
      </h1>
      <form class="flex flex-row shadow" @submit.prevent="contactForm()">
        <input
          class="text-left shadow-md px-6 w-full border-2 font-bold font-serif rounded-xl h-14"
          v-model="newtodo"
          required
          placeholder="Add a new task........ "
        />
      </form>
      <div class="space-y-1 h-full overflow-auto">
        <div class="flex flex-col space-y-3">
          <div
            class="py-2 border-b flex items-center"
            v-for="todo in filteredtodos"
            :key="todo.id"
          >
            <div class="flex flex-col h-auto w-full px-2">
              <div class="flex">
                <!-- {{ todo.done }} -->
                <input
                  type="checkbox"
                  class="mr-4 flex-grow-0"
                  v-model="todo.done"
                  @change="gettodoClass(todo)"
                />
                <span
                  class="font-bold font-serif text-start flex-grow word-break-all"
                  :class="
                    todo.done ? 'line-through text-blue-600' : 'text-black'
                  "
                >
                  {{ todo.text }}
                </span>
                <div class="space-x-2 flex flex-row">
                  <button class="w-6 opacity-60" @click="removeTodo(todo)">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                      <path
                        fill="black"
                        d="M19 4h-3.5l-1-1h-5l-1 1H5v2h14M6 19a2 2 0 0 0 2 2h8a2 2 0 0 0 2-2V7H6z"
                      />
                    </svg>
                  </button>

                  <!-- tạo ra nút màu đỏ -->
                  <button @click="favoritesTodo(todo)">
                    <svg
                      class="w-5"
                      :class="todo.favorites ? 'text-red-500' : 'opacity-60 '"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 24 24"
                    >
                      <path
                        fill="currentColor"
                        d="m12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5C2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3C19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54z"
                      />
                    </svg>
                  </button>
                  <button @click="arrangeTodo()">
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      width="1.2em"
                      height="1.2em"
                      viewBox="0 0 256 256"
                    >
                      <path
                        fill="black"
                        d="M76 92a16 16 0 1 1-16-16a16 16 0 0 1 16 16m52-16a16 16 0 1 0 16 16a16 16 0 0 0-16-16m68 32a16 16 0 1 0-16-16a16 16 0 0 0 16 16M60 148a16 16 0 1 0 16 16a16 16 0 0 0-16-16m68 0a16 16 0 1 0 16 16a16 16 0 0 0-16-16m68 0a16 16 0 1 0 16 16a16 16 0 0 0-16-16"
                      />
                    </svg>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div>
        <div class="flex flex-row space-x-1 justify-end">
          <div class="flex flex-row font-serif text-right">You have</div>
          <p id="countFalseDisplay" class="font-bold space-x-3 text-right"></p>
          <div>tasks left todo</div>
        </div>
        <div class="text-end mt-4 space-x-2">
          <button
            class="bg-green-500 font-serif hover:bg-green-700 duration-500 text-white border-double border-4 p-0 rounded-xl w-20"
            @click="hideCompleted = false"
          >
            Show All
          </button>
          <button
            class="bg-blue-500 font-serif hover:bg-blue-700 duration-500 text-white p-0 rounded-xl border-double border-4 w-20"
            @click="hideCompleted = true"
          >
            Hide
          </button>
          <button
            class="bg-red-500 font-serif hover:bg-red-700 duration-500 text-white p-0 rounded-xl border-double border-4 w-20"
            @click="showFavorites"
          >
            Favorites
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
