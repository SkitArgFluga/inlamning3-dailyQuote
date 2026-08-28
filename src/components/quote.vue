<script setup lang="ts">
import { ref, onMounted } from 'vue'

const quote = ref('')
const quotes = ref<string[]>([])

async function loadQuotes() {
  const response = await fetch('/quotes.txt')
  const text = await response.text()

  quotes.value = text
    .split('\n')
    .filter(line => line.trim() !== '')

  showDailyQuote()
}

function showDailyQuote() {
  const day = new Date().getDate()
  const index = day % quotes.value.length

  quote.value = quotes.value[index]
}

function newQuote() {
  const index = Math.floor(
    Math.random() * quotes.value.length
  )

  quote.value = quotes.value[index]
}

onMounted(() => {
  loadQuotes()
})
</script>

<template>
  <section class="quote">
    <h2>Today's Quote</h2>

    <p v-if="quote">
      "{{ quote }}"
    </p>

    <p v-else>
      Loading quote...
    </p>

    <button @click="newQuote">
      New Quote
    </button>
  </section>
</template>