<script setup>

import { ref } from 'vue';
const quotes = [
  "The only limit to our realization of tomorrow is our doubts of today.",
  "Do not wait to strike till the iron is hot, but make it hot by striking.",
  "The future belongs to those who believe in the beauty of their dreams.",
  "It does not matter how slowly you go as long as you do not stop.",
  "Success is not final, failure is not fatal: It is the courage to continue that counts."
];

const currentQuote = ref(quotes[0]);

function generateQuote() {
  const randomIndex = Math.floor(Math.random() * quotes.length)
  currentQuote.value = quotes[randomIndex]
}

function copyToClipboard() {
  navigator.clipboard.writeText(currentQuote.value)
    .then(() => alert('Quote copied to clipboard!'))
    .catch(() => alert('Failed to copy quote to clipboard.'));
}


</script>

<template>

  <h2>Random Quote Generator</h2>
  <div class="quote-container">
    <p class="quote-text">"{{  currentQuote }}"</p>
    <div class="buttons">
      <button @click="generateQuote">New quote</button>
      <button @click="copyToClipboard">Copy to clipboard</button>
    </div>
  </div>
</template>

<style>

h2{
  text-align: center;
  margin-top: 10px;
  color: white;
}
.quote-container {
  text-align: center;
  max-width: 500px;
  margin: 100px auto;
  font-family: sans-serif;
}

.quote-text {
  font-size: 1.5rem;
  margin-bottom: 1rem;
}

.buttons button {
  margin: 0 0.5rem;
  padding: 0.5rem 1rem;
  font-size: 1rem;
}

</style>
