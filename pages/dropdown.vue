<script setup>
const isOpen = ref(false);

function toggleDropdown() {
  this.isOpen = !this.isOpen;
  console.log("🚀 ~ toggleDropdown ~ this.isOpen:", this.isOpen);
}
</script>

<template>
  <div class="h-screen w-screen bg-blue-600 flex justify-center items-center">
    <div>
      <button
        @click="toggleDropdown()"
        type="button"
        class="flex justify-center w-36 rounded-md border border-gray-300 relative shadow-sm px-4 py-2 bg-blue-900 text-sm font-medium text-white hover:bg-blue-500"
        aria-expanded="true"
        aria-haspopup="true"
      >
        Options
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
      class="absolute w-56 bottom-44 shadow-lg rounded-md border bg-white flex flex-col pace-y-2"
    >
      <!-- edit -->
      <button
        class="hover:bg-blue-400 h-8 rounded-md pl-2 flex justify-start items-center"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="1.2em"
          class=""
          height="1.2em"
          viewBox="0 0 24 24"
        >
          <path
            fill="black"
            d="M3 21v-4.25L16.2 3.575q.3-.275.663-.425t.762-.15t.775.15t.65.45L20.425 5q.3.275.438.65T21 6.4q0 .4-.137.763t-.438.662L7.25 21zM17.6 7.8L19 6.4L17.6 5l-1.4 1.4z"
          />
        </svg>
        <div class="flex-auto">Edit</div>
      </button>

      <!-- duplicate -->
      <button
        class="hover:bg-blue-400 h-8 rounded-md pl-2 flex justify-start items-center"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="1.2em"
          height="1.2em"
          viewBox="0 0 24 24"
        >
          <path
            fill="black"
            d="M5 3h12v4h4v14H7v-4H3V3zm10 4V5H5v10h2V7zM9 17v2h10V9H9z"
          />
        </svg>
        <div class="flex-auto">Duplicate</div>
      </button>

      <!-- archive -->
      <button
        class="hover:bg-blue-400 h-8 rounded-md pl-2 flex justify-start items-center"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="1.2em"
          height="1.2em"
          viewBox="0 0 24 24"
        >
          <path
            fill="black"
            d="M2 5c0-.943 0-1.414.293-1.707C2.586 3 3.057 3 4 3h16c.943 0 1.414 0 1.707.293C22 3.586 22 4.057 22 5c0 .943 0 1.414-.293 1.707C21.414 7 20.943 7 20 7H4c-.943 0-1.414 0-1.707-.293C2 6.414 2 5.943 2 5"
          />
          <path
            fill="black"
            fill-rule="evenodd"
            d="M20.069 8.5c.141 0 .286 0 .431-.002V13c0 3.771 0 5.657-1.172 6.828C18.157 21 16.271 21 12.5 21h-1c-3.771 0-5.657 0-6.828-1.172C3.5 18.657 3.5 16.771 3.5 13V8.498c.145.002.29.002.431.002zM9 12c0-.466 0-.699.076-.883a1 1 0 0 1 .541-.541c.184-.076.417-.076.883-.076h3c.466 0 .699 0 .883.076a1 1 0 0 1 .54.541c.077.184.077.417.077.883s0 .699-.076.883a1 1 0 0 1-.541.54c-.184.077-.417.077-.883.077h-3c-.466 0-.699 0-.883-.076a1 1 0 0 1-.54-.541C9 12.699 9 12.466 9 12"
            clip-rule="evenodd"
          />
        </svg>
        <div class="flex-auto">Archive</div>
      </button>
      <!-- Move -->
      <button
        class="hover:bg-blue-400 h-8 rounded-md pl-2 flex justify-start items-center"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="1.2em"
          height="1.2em"
          viewBox="0 0 24 24"
        >
          <path
            fill="black"
            d="M5 21q-.825 0-1.412-.587T3 19v-3h2v3h14V7H5v3H3V5q0-.825.588-1.412T5 3h14q.825 0 1.413.588T21 5v14q0 .825-.587 1.413T19 21zm6.5-3.5l-1.4-1.4l2.075-2.1H3v-2h9.175L10.1 9.9l1.4-1.4L16 13z"
          />
        </svg>
        <div class="flex-auto">Move</div>
      </button>
      <!-- Delete -->
      <button
        class="hover:bg-blue-400 h-8 rounded-md pl-2 flex justify-start items-center"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class=""
          width="1.2em"
          height="1.2em"
          viewBox="0 0 12 12"
        >
          <path
            fill="black"
            d="M5 3h2a1 1 0 0 0-2 0M4 3a2 2 0 1 1 4 0h2.5a.5.5 0 0 1 0 1h-.441l-.443 5.17A2 2 0 0 1 7.623 11H4.377a2 2 0 0 1-1.993-1.83L1.941 4H1.5a.5.5 0 0 1 0-1zm3.5 3a.5.5 0 0 0-1 0v2a.5.5 0 0 0 1 0zM5 5.5a.5.5 0 0 0-.5.5v2a.5.5 0 0 0 1 0V6a.5.5 0 0 0-.5-.5"
          />
        </svg>
        <div class="flex-auto">Delete</div>
      </button>
    </div>
  </div>
</template>
