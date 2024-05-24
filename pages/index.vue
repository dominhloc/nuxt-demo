<script setup>
const player = ref("X");
//
const board = ref([
  ["", "", ""],
  ["", "", ""],
  ["", "", ""],
]);

const lines = [
  [0, 1, 2],
  [3, 4, 5],
  [6, 7, 8],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8],
  [0, 4, 8],
  [2, 4, 6],
];

function checkWinner(board) {
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];

    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
      return board[a];
    }
  }
  return null;
}

const winner = computed(() => checkWinner(board.value.flat()));

function MakeMove(x, y) {
  if (winner.value) return;
  if (board.value[x][y]) return;
  board.value[x][y] = player.value;
  player.value = player.value === "X" ? "O" : "X";
  //console.log("🚀 ~ MakeMove ~ player.value:", player.value);
}

function Reset() {
  //console.log("🚀 ~ Reset ~ Reset:", Reset);
  board.value = [
    ["", "", ""],
    ["", "", ""],
    ["", "", ""],
  ];
  player.value = "X";
}
</script>

<template>
  <div
    class="bg-slate-600 h-screen w-screen flex flex-col justify-center overflow-auto items-center space-y-8"
  >
    <h1 class="text-6xl font-serif text-yellow-200">TIC TAC TOE</h1>
    <div
      class="text-white flex justify-center items-center space-x-3 text-4xl font-serif"
    >
      <div>Player</div>
      <div class="text-6xl text-yellow-200">{{ player }}</div>
      's
      <div>Turn</div>
    </div>

    <div
      class="flex flex-col p-9 space-y-3 border-2 border-dashed border-yellow-400 rounded-xl"
    >
      <div v-for="(row, x) in board" key="x" class="flex space-x-3">
        <div
          v-for="(cell, y) in row"
          key="y"
          @click="MakeMove(x, y)"
          :class="`w-24 h-24 bg-yellow-200 border border-yellow-400 flex justify-center items-center hover:bg-yellow-500 rounded-xl ${
            cell === 'X'
              ? 'text-blue-500 text-6xl font-bold'
              : 'text-red-500 text-6xl font-bold'
          }`"
        >
          {{ cell === "X" ? "X" : cell === "O" ? "O" : "" }}
        </div>
      </div>
    </div>
    <div v-if="winner">
      <div
        class="text-white font-serif text-5xl flex justify-center items-center space-x-3"
      >
        <div>🎉Player</div>
        <div class="text-7xl text-yellow-200">{{ winner }}</div>
        <div>Wins🎉</div>
      </div>
    </div>

    <div class="flex justify-center">
      <button
        class="w-32 rounded-xl hover:bg-slate-500 text-2xl font-serif text-yellow-200 border-yellow-200 border-2 border-dashed font-bold pt-1"
        @click="Reset"
      >
        Restart
      </button>
    </div>
  </div>
</template>
