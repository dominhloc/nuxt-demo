<script setup>
import { ref, computed } from "vue";

let id = 1;
const newTodo = ref("");
const hideCompleted = ref(false);
const todos = ref([
    { id: id++, text: "Công Việc 1", done: false },
    { id: id++, text: "Công Việc 2", done: false },
    { id: id++, text: "Công Việc 3", done: false },
    { id: id++, text: "Công Việc 4", done: false },
    { id: id++, text: "Công Việc 5", done: false },
    { id: id++, text: 'Công Việc 6', done: false },
    { id: id++, text: 'Công Việc 7', done: false },
    { id: id++, text: 'Công Việc 8', done: false },
    { id: id++, text: 'Công Việc 9', done: false }
]);

const filteredTodos = computed(() => {
    return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});

function addTodo() {
    todos.value.push({
        id: id++,
        text: newTodo.value,
        done: false,
    });
    console.log("🚀 ~ todos.value:", todos.value);
    newTodo.value = "";
}

function removeTodo(todo) {
    console.log("🚀 ~ todo:", todo);
    todos.value = todos.value.filter((t) => t !== todo);
}

function getTodoClass(todo) {
    if (todo.done) {
        return "line-through";
    } else {
        return "text-red-50";
    }
}
</script>

<template>
    <div class="bg-blue-400 h-screen flex flex-col justify-center items-center">
        <div class="container mx-auto p-4 flex flex-col bg-white h-[600px] w-[450px] 
        space-y-3 rounded-xl shadow-md justify-between">
            <h1 class=" text-3xl text-center font-bold ">Todo App</h1>
            <form class="flex flex-row shadow" @submit.prevent="addTodo">
                <input class="text-left px-6 w-full border-2 font-bold rounded-xl h-14" v-model="newTodo" required
                    placeholder="Add a new task........ " />
            </form>
            <div class="space-y-5 h-full overflow-auto">
                <div class="flex flex-col">
                    <div class="py-2 border-b flex items-center" v-for="todo in filteredTodos" :key="todo.id">
                        <div class="flex flex-col h-auto w-full px-2">
                            <div class="flex items-center justify-between">
                                <input type="checkbox" class="mr-2 flex-grow-0" v-model="todo.done" />
                                <span class="!text-black font-bold text-start flex-grow word-break-all"
                                    :class="getTodoClass(todo)">{{ todo.text }}
                                </span>
                                <button class="rounded flex-grow-0 w-5 bg-red-500 text-white"
                                    @click="removeTodo(todo)"><img
                                        src="https://banner2.cleanpng.com/20180204/tew/kisspng-button-icon-delete-button-png-picture-5a77bb72658409.7623834215177962104158.jpg"
                                        class="w-5 h-5 rounded"></button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="text-end mt-4 space-x-2">
                <button class="bg-green-500 hover:bg-green-600 duration-500 text-white p-1 rounded-xl w-20"
                    @click="hideCompleted = false">Show All</button>
                <button class="bg-blue-500 hover:bg-blue-600 duration-500 text-white p-1 rounded-xl w-20"
                    @click="hideCompleted = true">Hide</button>
            </div>
        </div>
    </div>
</template>
