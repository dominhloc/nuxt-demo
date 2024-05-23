<script setup>
// khai báo người chơi đầu tiên
let player = ref("O");
// khai báo tạo bảng cờ
const board = ref([
  ["", "", ""],
  ["", "", ""],
  ["", "", ""],
]);
//check điều kiện chiến thắng
const checkWinner = (board) => {
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
    const [a, b, c] = lines[i];
    if (board[a] && board[a] === board[b] && board[a] === board[c])
      return board[a];
  }
  return null;
};
// khai báo người chơi đầu tiên

// trả về giá trị của hàm checkWinner -- và dùng flat để làm phẳng mảng
const winner = computed(() => checkWinner(board.value.flat()));

// xử lý các nước đi trong game
const MakeMove = (x, y) => {
  // nếu có
  if (winner.value) return;
  //k.tra các ô
  if (board.value[x][y]) return;
  //
  board.value[x][y] = player.value;
  //
  player.value = player.value === "X" ? "O" : "X";
};
const Reset = () => {
  board.value = [
    ["", "", ""],
    ["", "", ""],
    ["", "", ""],
  ];
  player.value = "O";
};
</script>

<template>
  <div class="flex space-x-3 rounded-xl">
    <div v-for="(row, x) in board" :key="x" class="space-y-3">
      <div
        v-for="(cell, y) in row"
        :key="y"
        @click="MakeMove(x, y)"
        :class="`border-white shadow-2xl h-24 w-24 rounded-2xl hover:bg-slate-300 ${
          cell === 'X' ? 'text-orange-500 text-2xl' : 'text-blue-500 text-2xl'
        }`"
      >
        {{ cell === "X" ? "X" : cell === "O" ? "O" : "" }}
      </div>
    </div>
    player {{ winner }} winner
  </div>
  <button @click="Reset">new game</button>
  <!-- <h1>🎉 Congratulations!</h1> -->
</template>
