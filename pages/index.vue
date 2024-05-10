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
]);

const filteredTodos = computed(() => {
    return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});

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
    let x = todos.value.filter((t) => t.id !== todo.id);
    todos.value = x
}

function getTodoClass(todo) {
    if (todo.done) {
        return "line-through text-red-500";
    } else {
        return "text-black-500";
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
            <div class="space-y-5 h-full overflow-auto">
                <div class="flex flex-col">
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
            </div>
        </div>
    </div>
</template>
