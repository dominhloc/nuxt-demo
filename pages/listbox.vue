<script setup>
const isOpen = ref(false);
const people = ref([
  { id: 1, name: "Cầu thủ A", favorite: false },
  { id: 2, name: "Cầu thủ B", favorite: false },
  { id: 3, name: "Cầu thủ C", favorite: false },
  { id: 4, name: "Cầu thủ D", favorite: false },
]);

function toggleDropdown() {
  this.isOpen = !this.isOpen;
  console.log("🚀 ~ toggleDropdown ~ this.isOpen:", this.isOpen);
}

function push(person) {
  let x = person.id;
  console.log("🚀 ~ push ~ x:", x);
}
</script>

<template>
  <div class="h-screen w-screen bg-blue-600 flex justify-center items-center">
    <div>
      <button
        @click="toggleDropdown()"
        type="submit"
        class="flex justify-center w-36 rounded-md border border-gray-300 relative shadow-sm px-4 py-2 bg-blue-900 text-sm font-medium text-white hover:bg-blue-500"
        aria-expanded="true"
        aria-haspopup="true"
      >
        {{ people.name }}
        <svg
          class="mr-1 ml-2 h-5 w-5"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 20 20"
          fill="currentColor"
          aria-hidden="true"
        >
          <path
            fill-rule="evenodd"
            d="M5.293 9.707a1 1 0 011.414 0L10 13.086l3.293-3.379a1 1 0 111.414 1.414l-4 4.086a1 1 0 01-1.414 0l-4-4.086a1 1 0 010-1.414z"
            clip-rule="evenodd"
          />
        </svg>
      </button>
    </div>

    <div
      v-if="isOpen"
      class="absolute bottom-48 space-y-3 shadow-lg rounded-md flex flex-col pace-y-2"
    >
      <div class="flex-col flex justify-center items-center space-y-2">
        <button
          v-for="person in people"
          @click="push(person)"
          class="hover:bg-slate-300 flex w-72 border-2 bg-slate-100 rounded-lg"
          key="person.id"
          value="person"
        >
          id: {{ person.id }} --- {{ person.name }}
        </button>
      </div>
    </div>
  </div>
</template>
