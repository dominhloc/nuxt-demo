<script setup>
import { ref, computed } from "vue";

let id = 0

const message = ref('Danh Sách Các Việc Cần Làm')
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
    <div class="bg-white-400 w-full h-screen flex flex-col justify-center items-center">
        <div class="p-10 bg-white shadow-xl border rounded-xl text-black">

            <h1 class="text-center text-4xl text-black-600 font-bold">{{ message }}</h1>


            <form class="text-center" @submit.prevent="addTodo">
                <input v-model="newTodo" required placeholder="Thêm công việc">
                <button>Thêm</button>
            </form>

            <ul>
                <li class="text-center space-x-9" v-for="todo in filteredTodos" :key="todo.id">
                    <span class="!text-black " :class="getTodoClass(todo)">{{ todo.text }}</span>
                    <button class="text-red-600" @click="removeTodo(todo)"> Xóa </button>
                    <input type="checkbox" v-model="todo.done">
                </li>
            </ul>

            <div class="text-center">
                <button @click="hideCompleted = !hideCompleted">
                    {{ hideCompleted ? 'Hiển Thị Tất Cả' : 'Ẩn Việc Đã Làm' }}
                </button>
            </div>
        </div>
    </div>
</template>
