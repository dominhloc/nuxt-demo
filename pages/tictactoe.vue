<script setup>
// khai báo người chơi đầu tiên
let player = ref("O");
// khai báo tạo bảng cờ 3x3
const board = ref([
  ["", "", ""],
  ["", "", ""],
  ["", "", ""],
]);
const checkWinner = (board) => {
  //check điều kiện chiến thắng của các cột ngang , dọc , chéo
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
  // dùng for lặp qua mảng `lines` để kiểm tra điều kiện chiến thắng

  for (let i = 0; i < lines.length; i++) {
    //lấy ra các vị trí chiến thắng
    const [a, b, c] = lines[i];
    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
      return board[a]; // Trả về 'X' hoặc 'O' nếu có người chiến thắng
    }
  }
  return null; // Trả về null nếu không có người chiến thắng
};
// tại biến tính toán
const winner = computed(() => checkWinner(board.value.flat()));

// xử lý các bước đi trong game
const MakeMove = (x, y) => {
  if (winner.value) return;

  if (board.value[x][y]) return;

  board.value[x][y] = player.value;

  player.value = player.value === "X" ? "O" : "X";
};

// nút reset tra về giá trị ban đầu
const ResetGame = () => {
  board.value = [
    ["", "", ""],
    ["", "", ""],
    ["", "", ""],
  ];
  player.value = "O";
};
</script>

<template>
  <div
    class="flex flex-col justify-center items-center bg-blue-300 space-y-10 h-screen"
  >
    <div
      class="text-white text-5xl bg-white w-2/5 h-fit rounded-2xl font-bold font-serif flex justify-center items-center"
    >
      <div class="text-center text-blue-300">TIC TAC TOE</div>
    </div>
    <div class="text-center text-white text-2xl">
      Player "
      {{ player }}"
    </div>

    <div class="flex flex-col space-y-3">
      <div v-for="(row, x) in board" :key="x" class="flex space-x-3">
        <div
          v-for="(cell, y) in row"
          :key="y"
          @click="MakeMove(x, y)"
          :class="`border border-white w-36 h-36 flex rounded-2xl items-center bg-white hover:bg-slate-200 ${
            cell === 'X' ? 'text-pink-500 text-6xl' : 'text-blue-400 text-6xl'
          }`"
        >
          {{ cell === "X" ? "X" : cell === "O" ? "O" : "" }}
        </div>
      </div>
    </div>
    <div class="text-center">
      <h2 v-if="winner" class="text-6xl font-bold mb-8">
        Player '{{ winner }}' wins!
      </h2>
      <button @click="ResetGame">Reset</button>
    </div>
  </div>
</template>
