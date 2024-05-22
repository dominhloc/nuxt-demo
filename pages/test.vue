<script setup>
// khai báo người chơi đầu tiên
let player = ref("O");
// khai báo tạo bảng cờ 3x3
const board = ref([
  ["", "", ""],
  ["", "", ""],
  ["", "", ""],
]);
// check các điều kiện chiến thắng
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
    // lấy ra các vị trí chiến thắng
    const [a, b, c] = lines[i];

    // kiểm tra a,b,c có cùng giá trị hay không. Nếu cả 3 điều kiện đúng thì thỏa mãn 1 đk chiến thắng
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
    ["", "", ""],
    ["", "", ""],
    ["", "", ""],
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
      <h1 class="font-serif font-bold text-blue-400 text-center text-4xl">
        TIC TAC TOE
      </h1>
    </div>
    <div
      class="w-1/3 h-14 text-2xl font-serif space-x-3 rounded-xl text-white flex justify-center items-center"
    >
      <div>Player</div>
      <div class="text-red-500 text-4xl">{{ player }}'s</div>
      <div>Turn</div>
    </div>
    <div class="flex space-x-3">
      <div v-for="(row, x) in board" :key="x" class="space-y-3">
        <div
          v-for="(cell, y) in row"
          :key="y"
          @click="MakeMove(x, y)"
          :class="`border border-white bg-slate-100 h-32 w-32 rounded-2xl flex justify-center items-center hover:bg-slate-300 ${
            cell === 'X' ? 'text-orange-500 text-6xl' : 'text-blue-500 text-6xl'
          }`"
        >
          {{ cell === "X" ? "X" : cell === "O" ? "O" : "" }}
        </div>
      </div>
    </div>
    <div v-if="winner">
      <div
        class="w-auto h-14 rounded-xl text-5xl text-center flex justify-center items-center font-serif font-bold text-white"
      >
        Player {{ winner }} Winner
      </div>
    </div>
    <!-- tạo nút reset bằng button  -->
    <button
      class="border border-1 w-36 h-10 text-xl font-serif font-bold text-blue-400 bg-white rounded-xl hover:bg-slate-300 duration-500"
      @click="ResetGame"
    >
      Game New
    </button>
  </div>
</template>
