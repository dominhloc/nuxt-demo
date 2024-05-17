<script setup>
import { ref, computed } from "vue";

const newtodo =ref('');
const hideCompleted = ref(false);
const todos = ref([
   { id: 1, text: "Công Việc 1", done: false, favorites: false },
   { id: 2, text: "Công Việc 2", done: false, favorites: false },
   { id: 3, text: "Công Việc 3", done: false, favorites: false },
   { id: 4, text: "Công Việc 4", done: false, favorites: false },
]);

</script>
<template></template>
