<script setup>
import { ref, computed } from "vue";

let id = 0;
let playEr1 = "X";
let playEr2 = "O";
const board = [
  ["", "", ""],
  ["", "", ""],
  ["", "", ""],
];
</script>

<template>
  <div class="flex flex-col justify-center items-center bg-cyan-950 h-screen">
    <div
      class="h-[100px] w-[300px] text-white text-5xl font-bold flex flex-col"
    >
      <div class="justify-between text-center">TIC TAC TOE</div>
    </div>

    <div class="border-white bg-slate-500 border-2 rounded-xl p-5 shadow">
      <div class="text-center text-white mb-15 text-2xl">
        Lượt Người Chơi 'X'
        <div
          class="m-5 flex flex-col justify-center items-center h-xs w-xs text-center bg-black rounded-xl"
        ></div>
        <div
          class="mx-auto p-4 flex flex-col bg-white h-[300px] w-[300px] rounded-xl"
        ></div>

        <button
          class="p-2 bg-cyan-500 duration-100 shadow-lg shadow-cyan-200 hover:bg-cyan-600 rounded-2xl"
          @click="hideCompleted = false"
        >
          Bat Dau Lai
        </button>
      </div>
    </div>
  </div>
</template>
