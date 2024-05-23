<script setup>
//
import JSConfetti from "js-confetti";
const confetti = new JSConfetti();

function showConfetti() {
  confetti.addConfetti();
}

// khai báo người chơi đầu tiên
let player = ref("O");
// khai báo tạo bảng cờ 3x3 hoặc 4x4
const board = ref([
  ["", "", "", ""],
  ["", "", "", ""],
  ["", "", "", ""],
  ["", "", "", ""],
]);
// check các điều kiện chiến thắng
const checkWinner = (board) => {
  //các điều kiện chiến thắng
  const lines = [
    //dọc
    [0, 1, 2],
    [4, 5, 6],
    [8, 9, 10],
    [12, 13, 14],
    [1, 2, 3],
    [5, 6, 7],
    [9, 10, 11],
    [13, 14, 15],
    //ngang
    [0, 4, 8],
    [1, 5, 9],
    [2, 6, 10],
    [3, 7, 11],
    [4, 8, 12],
    [5, 9, 13],
    [6, 10, 14],
    [7, 11, 15],
    //chéo 1
    [1, 6, 11],
    [0, 5, 10],
    [5, 10, 15],
    [4, 9, 14],
    //chéo 2
    [2, 5, 8],
    [6, 9, 12],
    [3, 6, 9],
    [7, 10, 13],
  ];
  // dùng for lặp qua mảng `lines` để kiểm tra điều kiện chiến thắng
  for (let i = 0; i < lines.length; i++) {
    // lấy ra các vị trí chiến thắng
    const [a, b, c] = lines[i];

    // kiểm tra a, b, c có cùng giá trị hay không. Nếu cả 3 điều kiện đúng thì thỏa mãn 1 đ.kiện chiến thắng
    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
      return board[a]; // trả về 'X' hoặc 'O' nếu có người chiến thắng
    }
  }
  return null; // trả về null nếu không có người chiến thắng
};
// trả về giá trị của hàm checkWinner -- và dùng flat để làm phẳng mảng
const winner = computed(() => checkWinner(board.value.flat()));

// xử lý các nước đi trong game
const MakeMove = (x, y) => {
  // nếu có người chiến thắng, game kết thúc , không cần thực hiện thêm bước nào
  if (winner.value) return;

  // kiểm tra ô đã được đánh dấu chưa
  if (board.value[x][y]) return;

  // đánh dấu ô với giá trị của người chơi hiện tại
  board.value[x][y] = player.value;

  //chuyển lượt tới ng tiếp theo
  player.value = player.value === "X" ? "O" : "X";
};

// nút reset trả về giá trị ban đầu

const ResetGame = () => {
  board.value = [
    ["", "", "", ""],
    ["", "", "", ""],
    ["", "", "", ""],
    ["", "", "", ""],
  ];
  player.value = "O";
};
</script>
<template>
  <div
    class="flex flex-col justify-center items-center bg-blue-400 space-y-7 h-screen"
  >
    <div
      class="flex flex-row justify-center items-center w-1/3 bg-white rounded-xl"
    >
      <h1
        class="font-serif font-bold text-blue-400 shadow-2xl text-center text-4xl"
      >
        TIC TAC TOE
      </h1>
    </div>
    <div
      class="w-1/3 h-14 text-2xl font-serif space-x-3 border-2 font-bold rounded-xl text-white flex justify-center items-center"
    >
      <div>Player</div>
      <div class="text-red-500 text-5xl">{{ player }}'s</div>
      <div>Turn</div>
    </div>
    <div class="flex space-x-3 p-8 border-2 rounded-xl">
      <div v-for="(row, x) in board" :key="x" class="space-y-3">
        <div
          v-for="(cell, y) in row"
          :key="y"
          @click="MakeMove(x, y)"
          :class="`border border-white bg-slate-100 shadow-2xl text-black h-24 w-24 rounded-2xl flex justify-center items-center hover:bg-slate-300 ${
            cell === 'X' ? 'text-orange-500 text-6xl' : 'text-blue-500 text-6xl'
          }`"
        >
          {{ cell === "X" ? "X" : cell === "O" ? "O" : "" }}
        </div>
      </div>
    </div>
    <div v-if="winner">
      <div
        class="flex flex-row w-auto space-y-3 rounded-xl text-4xl space-x-3 text-center justify-center items-center font-serif font-bold text-white"
      >
        <div>🎉Player</div>
        <div class="text-red-500 text-6xl">{{ winner }}</div>
        <div>Winner🎉</div>
        {{ showConfetti() }}
      </div>
      <div class="font-serif text-center pt-3 text-white text-3xl">
        🥳Congratulation🥳
      </div>
    </div>
    <!-- tạo nút reset bằng button  -->
    <button
      class="border border-1 w-36 h-10 text-xl font-serif font-bold shadow-2xl text-blue-400 bg-white rounded-xl hover:bg-slate-300 duration-500"
      @click="ResetGame"
    >
      Game New
    </button>
    <!-- <h1 class="text-center" @click="showConfetti">🎉Congratulations🎉</h1> -->
  </div>
</template>
