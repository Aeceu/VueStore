<template>
  <nav class="w-full h-20 flex items-center gap-8 px-8 shadow-lg">
    <h1 class="text-emerald-500 font-extrabold text-2xl">TheDailyFind</h1>
    <div>
      <input v-model="search" placeholder="Search an item" class="border px-3 py-1 rounded-full" />
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const search = ref<string>('')
</script>

<style scoped></style>
