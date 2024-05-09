<script setup>
import { ref, computed } from "vue";

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
    { id: id++, text: 'Công Việc 1', done: false },
    { id: id++, text: 'Công Việc 2', done: false },
    { id: id++, text: 'Công Việc 3', done: false },
    { id: id++, text: 'Công Việc 4', done: false },
    { id: id++, text: 'Công Việc 5', done: false },
])

const filteredTodos = computed(() => {
    return hideCompleted.value
        ? todos.value.filter((t) => !t.done)
        : todos.value
})

function addTodo() {
    todos.value.push({
        id: id++, text: newTodo.value, done: false
    })
    newTodo.value = ''
}

function removeTodo(todo) {
    todos.value = todos.value.filter((t) => t !== todo)
}

function getTodoClass(todo) {
    if (todo.done) {
        return 'line-through'
    } else {
        return "text-red-50"
    }
}

</script>


<template>
    <div class="bg-blue-200 h-screen flex flex-col justify-center items-center">

        <div class="container mx-auto p-4 bg-white"><br>
            <h1 class=" text-3xl px-10 text-left font-bold ">Todo App</h1>
            <form class="flex flex-row px-10 gap-2 " @submit.prevent="addTodo">
                <input class=" bg-slate-300 text-right px-6 w-full font-bold" v-model="newTodo" required
                    placeholder="Add your new todo">
                <button class="bg-blue-500 text-white p-4 font-bold text-2xl">+</button>
            </form><br>

            <ul>

                <li v-for="todo in filteredTodos" :key="todo.id">

                    <div class="flex flex-col h-auto w-full px-10">
                        <div class="flex items-center mb-3">
                            <input type="checkbox" class="mr-2 flex-grow-0" v-model="todo.done">
                            <span class="!text-black font-bold text-start flex-grow word-break-all"
                                :class="getTodoClass(todo)">{{
                                    todo.text }}
                            </span>
                            <button class="text-white rounded mr-5 flex-grow-0 w-16" @click="removeTodo(todo)"><img
                                    src="https://banner2.cleanpng.com/20180204/tew/kisspng-button-icon-delete-button-png-picture-5a77bb72658409.7623834215177962104158.jpg"
                                    class="w-5 h-5 rounded"></button>
                        </div>
                    </div>
                </li>
            </ul>
            <br>
            <div class="text-end px-10 ">
                <button class="bg-green-500 text-white p-2 rounded mr-2" @click="hideCompleted = false">Show
                    All</button>
                <button class="bg-blue-500 text-white p-2 rounded " @click="hideCompleted = true">Hide</button>
            </div>
        </div>
    </div>

</template>
