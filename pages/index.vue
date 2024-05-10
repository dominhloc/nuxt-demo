<script setup>
import { ref, computed } from "vue";

const newTodo = ref("");
const hideCompleted = ref(false);

const todos = ref([
    { id: 1, text: "Công Việc 1", done: false },
    { id: 2, text: "Công Việc 2", done: false },
    { id: 3, text: "Công Việc 3", done: false },
    { id: 4, text: "Công Việc 4", done: false },
    { id: 5, text: "Công Việc 5", done: false },
    { id: 6, text: "Công Việc 6", done: false },
    { id: 7, text: "Công Việc 7", done: false },
    { id: 8, text: "Công Việc 8", done: false },
]);

const filteredTodos = computed(() => {
    return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});
//console.log("🚀 ~ filteredTodos ~ filteredTodos:", filteredTodos)

function addTodo() {
    let newIndex = todos.value.length + 1
    todos.value.push({
        id: newIndex,
        text: newTodo.value,
        done: false,
    });
    // console.log(todos.value)
    // xóa input đầu vào
    newTodo.value = "";
}

function removeTodo(todo) {
    let x = todos.value.filter((t) => t.id !== todo.id); //todo.id = giá trị của id
    //console.log("🚀 ~ todo.id:", todo.id)
    todos.value = x
}


function getTodoClass(todo) {
    if (todo.done) {
        //console.log("🚀 ~ getTodoClass ~ todo.done:", todo.done)
        return "line-through";
    }
}

function deleteAll() {
    let y = todos.value.filter((t) => t.id === newTodo)
    // mảngkhaibáo.value.filter(( giá trị trả về sẽ là t ) => nếu id = với newTodo là tệp rỗng )
    todos.value = y
}

function favoritesTodo(todo) {
    if (todo.done) {
        return "bg-red-500"
    }
}

</script>

<template>
    <div class="bg-cyan-900 h-screen flex flex-col justify-center items-center">
        <div class="container mx-auto p-4 flex flex-col bg-white h-[600px] w-[450px] 
        space-y-3 rounded-xl justify-between">
            <h1 class=" text-3xl text-center font-bold  hover:bg-gray-300 duration-500 ">Todo App</h1>
            <form class="flex flex-row shadow" @submit.prevent="addTodo">
                <input class="text-left shadow-md px-6 w-full border-2 font-bold rounded-xl h-14" v-model="newTodo"
                    required placeholder="Add a new task........ " />
            </form>
            <div class=" space-y-5 h-full overflow-auto">
                <div class="flex flex-col  hover:bg-slate-300 duration-500 space-y-2">
                    <div class="py-2 border-b flex items-center" v-for="todo in filteredTodos" :key="todo.id">
                        <div class="flex flex-col h-auto w-full px-2">
                            <div class="flex items-center justify-between">
                                <input type="checkbox" class="mr-2 flex-grow-0" v-model="todo.done" />
                                <span class="font-bold text-start flex-grow word-break-all"
                                    :class="getTodoClass(todo)">{{ todo.text }}
                                </span>
                                <button class="flex-grow-0 w-6" @click="removeTodo(todo)"><img
                                        src="https://banner2.cleanpng.com/20180204/tew/kisspng-button-icon-delete-button-png-picture-5a77bb72658409.7623834215177962104158.jpg"
                                        class="w-5 h-5 rounded"></button>

                                <svg :class="favoritesTodo(todo)" xmlns="http://www.w3.org/2000/svg" width="25"
                                    height="25" viewBox="0 0 24 24">
                                    <path fill="currentColor"
                                        d="m12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5C2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3C19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54z" />
                                </svg>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="text-end mt-4 space-x-2">
                <button class=" bg-green-500 hover:bg-green-600 duration-500 text-white p-1 rounded-xl w-20"
                    @click="hideCompleted = false">Show All</button>
                <button class="bg-blue-500 hover:bg-blue-600 duration-500 text-white p-1 rounded-xl w-20"
                    @click="hideCompleted = true">Hide</button>
                <button class=" bg-gray-500 hover:bg-gray-600 duration-500 text-white p-1 rounded-xl w-20"
                    @click="deleteAll">Delete All</button>
            </div>
        </div>
    </div>
</template>
