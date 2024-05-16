<!-- <script>
export default {
    data() {
        return {
            showFavorites: false,
            favoriteList: [
                { id: 1, name: 'Sản phẩm 1' },
                { id: 2, name: 'Sản phẩm 2' },
                { id: 3, name: 'Sản phẩm 3' },
                { id: 4, name: 'Sản phẩm 4' },
                { id: 5, name: 'Sản phẩm 5' },
            ],
        };
    },
};
</script>

// function deleteAll() {
//   let y = todos.value.filter((t) => t.id === newtodo);
//   // mảngkhaibáo.value.filter(( giá trị trả về sẽ là t ) => nếu id = với newtodo là tệp rỗng )
//   todos.value = y;
// }

// dùng for lặp qua từng id rồi xóa
// async function deleteAll() {
//   for (let i = 0; i < todos.id.length; i++);
//   {
//     x = todos.value;
//   }
//   console.log("🚀 ~ deleteAll ~ deleteAll:", x);
// const res = await $fetch(
//   `https://6642ea4a3c01a059ea20c7c2.mockapi.io/TODOLIST/${todo?.id}`,
//   {
//     method: `DELETE`,
//   }
// );
// todos.value = await $fetch(
//   "https://6642ea4a3c01a059ea20c7c2.mockapi.io/TODOLIST" // đặt lại mảng ban đầu
// );
// todos.value = undefined;
//}
 <button
          class="bg-gray-500 hover:bg-gray-600 duration-500 text-white p-1 rounded-xl w-20"
          @click="deleteAll"
        >
          Delete All
        </button> 

<template>
  <div>
    <button @click="showFavorites = !showFavorites">
      {{
        showFavorites ? "Ẩn Danh Sách Yêu Thích" : "Hiện Danh Sách Yêu Thích"
      }}
    </button>
    <ul v-if="showFavorites">
      <li v-for="item in favoriteList" :key="item.id">
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>
-->
<template>
  <div>
    <button @click="toggleVisibility">
      {{ isVisible ? "Ẩn" : "Hiện" }} nội dung
    </button>
    <p v-if="isVisible">Nội dung được hiển thị</p>
  </div>
</template>

<script script>
export default {
  data() {
    return {
      isVisible: false,
    };
  },
  methods: {
    toggleVisibility() {
      this.isVisible = !this.isVisible;
    },
  },
};
</script>
