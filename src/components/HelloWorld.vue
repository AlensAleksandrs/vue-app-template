<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()

const count = ref(0)
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">Number of clicks: {{ count }}</button>
  </div>

  <p class="read-the-docs">You've successfully launched the template!</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
