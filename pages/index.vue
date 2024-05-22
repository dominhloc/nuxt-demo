<script setup>
import JSConfetti from "js-confetti";

const confetti = new JSConfetti();

function showConfetti() {
  confetti.addConfetti({
    emojis: ["🌈", "⚡️", "💥", "✨", "💫", "🌸"],
  });
}

showConfetti();
</script>

<template>
  <h1 class="text-center" @click="showConfetti">🎉 Congratulations!</h1>
</template>
