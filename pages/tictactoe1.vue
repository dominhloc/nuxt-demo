<script setup>
//
import JSConfetti from "js-confetti";
const confetti = new JSConfetti();

function showConfetti() {
  confetti.addConfetti();
}
// khai báo người chơi đầu tiên
const player = ref("O");

// khai báo tạo bảng cờ 3x3
const board = ref([
  ["", "", ""],
  ["", "", ""],
  ["", "", ""],
]);

// tổ hợp các vị trí chiến thắng
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

// check điều kiện chiến thắng
function checkWinner(board) {
  // dùng for lặp qua mảng `lines` để kiểm tra điều kiện chiến thắng
  for (let i = 0; i < lines.length; i++) {
    //lấy ra vị trí chiến thắng
    const [a, b, c] = lines[i];

    //kiểm tra điều kiện a = b = c
    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
      // Trả về người chiến thắng 'X' hoặc 'O'
      return board[a];
    }
  }
  return null; // Trả về null nếu không có người chiến thắng
}

// tạo biến tính toán
const winner = computed(() => checkWinner(board.value.flat()));

// xử lý các bước đi trong game
function MakeMove(x, y) {
  // nếu có người chiến thắng - game kết thúc , không cần thực hiện thêm bước nào
  if (winner.value) return;

  // kiểm tra ô đã được đánh dấu chưa
  if (board.value[x][y]) return;

  // đánh dấu ô với giá trị của người chơi hiện tại
  board.value[x][y] = player.value;

  //chuyển lượt tới ng tiếp theo
  player.value = player.value === "X" ? "O" : "X";
}

// nút reset trả về giá trị ban đầu
function ResetGame() {
  board.value = [
    ["", "", ""],
    ["", "", ""],
    ["", "", ""],
  ];
  // trả về người chơi O đầu tiên
  player.value = "O";
}
</script>

<template>
  <div
    class="bg-sky-600 flex flex-col space-y-5 justify-center items-center h-screen w-screen"
  >
    <div class="text-center text-6xl text-white font-serif">TIC TAC TOE</div>
    <div
      class="text-3xl text-white font-serif flex justify-center items-center space-x-3"
    >
      <div>Player</div>
      <div class="text-6xl text-yellow-300">{{ player }}</div>
      's
      <div>Turn</div>
    </div>

    <div class="flex flex-col space-y-3">
      <div v-for="(row, x) in board" :key="x" class="flex space-x-3">
        <div
          v-for="(cell, y) in row"
          :key="y"
          @click="MakeMove(x, y)"
          :class="`border w-32 h-32 flex justify-center items-center rounded-2xl bg-white hover:bg-slate-300 ${
            cell === 'X'
              ? 'text-red-500 text-7xl font-bold'
              : 'text-blue-500 text-7xl font-bold'
          }`"
        >
          {{ cell === "X" ? "X" : cell === "O" ? "O" : "" }}
        </div>
      </div>
    </div>
    <div v-if="winner">
      <div
        class="text-white font-serif text-3xl flex flex-row justify-center items-center space-x-3"
      >
        <div>🎉 Player</div>
        <div class="text-yellow-300 font-bold text-5xl">
          {{ winner }}{{ showConfetti() }}
        </div>
        <div>Wins 🎉</div>
      </div>
    </div>
    <button
      class="text-slate-700 font-serif font-bold text-xl w-36 rounded-xl bg-white"
      @click="ResetGame"
    >
      New Game
    </button>
  </div>
</template>
