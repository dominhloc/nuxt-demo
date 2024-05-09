<script setup>
import { ref, computed } from 'vue'

let id = 0
let playEr1 = 'X'
let playEr2 = 'O'
const board = [
    ['', '', ''],
    ['', '', ''],
    ['', '', ''],
];

</script>


<template>

    < class="flex flex-col justify-center items-center bg-cyan-950 h-screen">
        <div class="flex flex-col justify-center items-center h-3xl w-3xl text-center">

            <div class="text-4xl mb-15 font-bold">TIC TAC TOE</div>

            <div class="border border-white border-2 rounded-xl p-5 shadow">

                <div class="text-center mb-15 text-2xl  ">Luot Nguoi Choi 'X'
                    <div
                        class="m-5 flex flex-col justify-center items-center h-xs w-xs text-center bg-black rounded-xl">
                    </div>

                    <button class="fixed bottom-66 p-2 bg-cyan-500 shadow-lg shadow-cyan-50/50 rounded-xl "
                        @click="hideCompleted = false">Bat Dau Lai</button>
                </div>
            </div>
        </div>
</template>