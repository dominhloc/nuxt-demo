<script setup>
// khai báo người chơi đầu tiên
const player = ref("O");
// khai báo tạo bảng cờ 3x3
const board = ref([
  ["", "", ""],
  ["", "", ""],
  ["", "", ""],
]);
// check điều kiện chiến thắng của các cột ngang , dọc , chéo
const checkWinner = (board) => {
  //tổ hợp các vị trí chiến thắng
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
    //lấy ra vị trí chiến thắng
    const [a, b, c] = lines[i];
    //kiểm tra điều kiện a = b = c
    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
      return board[a]; // Trả về người chiến thắng 'X' hoặc 'O'
    }
  }
  return null; // Trả về null nếu không có người chiến thắng
};

// tạo biến tính toán
const winner = computed(() => checkWinner(board.value.flat()));

// xử lý các bước đi trong game
const MakeMove = (x, y) => {
  if (winner.value) return;

  if (board.value[x][y]) return;

  // đánh dấu ô với giá trị của người chơi hiện tại
  board.value[x][y] = player.value;
  //chuyển lượt tới ng tiếp theo
  player.value = player.value === "X" ? "O" : "X";
};
// nút reset trả về giá trị ban đầu

function ResetGame() {
  board.value = [
    ["", "", ""],
    ["", "", ""],
    ["", "", ""],
  ];
  player.value = "O";
}
</script>

<template>
  <div class="text-center text-2xl">tictactoe</div>
  <div>Player {{ player }}'s turn</div>

  <div class="flex flex-col space-y-3">
    <div v-for="(row, x) in board" :key="x" class="flex space-x-3">
      <div
        v-for="(cell, y) in row"
        :key="y"
        @click="MakeMove(x, y)"
        :class="`border w-32 h-32  bg-white hover:bg-slate-200 ${
          cell === 'X' ? 'text-pink-500 text-xl' : 'text-blue-400 text-xl'
        }`"
      >
        {{ cell === "X" ? "X" : cell === "O" ? "O" : "" }}
      </div>
    </div>
  </div>
  <div class="text-center">Player {{ winner }} wins!</div>
  <button @click="ResetGame">New Game</button>
</template>
