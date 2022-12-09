<script setup>
import presentsData from './presents.json'
import { ref, computed } from 'vue'

const sorted = ref(false)

const toggleSort = () => (sorted.value = !sorted.value)

const presents = computed(() =>
  sorted.value
    ? [...presentsData].sort(
        (a, b) => a.dimensions.width * a.dimensions.height - b.dimensions.width * b.dimensions.height
      )
    : presentsData
)
</script>

<template>
  <div class="w-full h-full p-4 flex justify-center items-center">
    <div class="max-w-md">
      <div>
        <img src="/assets/tree.svg" alt="Christmas tree" />
      </div>
      <div class="mt-2 flex justify-center items-center">
        <img
          v-for="present in presents"
          :key="present.id"
          :src="present.src"
          :alt="`Present ${present.id}`"
          data-qa="present"
        />
      </div>
      <div class="flex justify-center mt-4">
        <button @click="toggleSort" class="btn-sort">Toggle sort</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.btn-sort {
  @apply px-4 py-2 rounded text-white font-bold bg-blue-800 hover:bg-blue-900;
}
</style>
