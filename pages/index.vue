<script setup>
import { ref, computed } from "vue";

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
    { id: id++, text: 'Viec 1', done: false },
    { id: id++, text: 'Viec 2', done: false },
    { id: id++, text: 'Viec 3', done: false },
    { id: id++, text: 'Viec 4', done: false },
    { id: id++, text: 'Viec 5', done: false },
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

// function lineThrough(todo) {
//     console.log("line throufgh cline", todo);
//     todo.done = !todo.done
//}

function getTodoClass(todo) {
    if (todo.done) {
        return 'line-through'
    } else {
        return "text-red-50"
    }
}

</script>


<template>
    <div class="bg-blue-200 w-full h-screen flex flex-col justify-center items-center">

        <div class="p-24 w-4/5 bg-white shadow-2xl border rounded-3xl">

            <h1 class="h-14 w-30 text-4xl bg-white-400 text-left font-bold ">Todo App</h1><br>

            <form class="flex" @submit.prevent="addTodo">
                <input class="text-left w-full font-bold" v-model="newTodo" required placeholder="Add your new todo">
                <button class="bg-blue-500 text-white p-4 font-bold text-2xl rounded-2xl">+</button>
            </form><br>

            <ul>

                <li v-for="todo in filteredTodos" :key="todo.id">

                    <div class="flex font-bold bg-gray-100">
                        <span class="!text-black" :class="getTodoClass(todo)">{{ todo.text }}</span>
                        <button class="text-white item-center bg-red-500 rounded" @click="removeTodo(todo)"> Xóa
                        </button>
                        <input type="checkbox" v-model="todo.done">
                    </div>
                </li>
            </ul><br>

            <div class="text-center">
                <button class="bg-blue-500 text-white p-2 rounded" @click="hideCompleted = !hideCompleted">
                    {{ hideCompleted ? 'Hiển Thị Tất Cả' : 'Ẩn Việc Đã Làm' }}
                </button>
            </div>
        </div>
    </div>

</template>
