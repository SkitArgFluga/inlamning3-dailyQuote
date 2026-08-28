<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const time = ref(new Date())

let timer: number

onMounted(() => {
  timer = window.setInterval(() => {
    time.value = new Date()
  }, 1000)
})

onUnmounted(() => {
  clearInterval(timer)
})
</script>

<template>
  <section class="clock">
    <p>
      {{
        time.toLocaleDateString('sv-SE', {
          weekday: 'long',
          day: 'numeric',
          month: 'long',
          year: 'numeric'
        })
      }}
    </p>

    <p>{{ time.toLocaleTimeString('sv-SE') }}</p>
  </section>
</template>