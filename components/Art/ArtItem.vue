<template>
  <div
    class="flex items-center bg-white rounded-2xl p-4 mb-4 transition-all duration-300 hover:transform hover:-translate-y-1 hover:shadow-lg animate-fadeIn"
  >
    <div class="w-[60px] h-[60px] rounded-xl overflow-hidden mr-4 flex-shrink-0">
      <img
        :src="item.image"
        :alt="item.title"
        class="w-full h-full object-cover"
      />
    </div>
    <div class="flex-1">
      <h3 class="text-base font-semibold mb-1">{{ item.title }}</h3>
      <p class="text-xs text-gray-500 mb-1">{{ item.description }}</p>
      <div class="text-sm font-semibold">{{ item.price }}</div>
    </div>
    <div class="ml-2.5">
      <ArrowRightIcon class="text-gray-500" />
    </div>
  </div>
</template>

<script setup>
import { ArrowRight as ArrowRightIcon } from 'lucide-vue-next'

defineProps({
  item: {
    type: Object,
    required: true,
  },
})
</script>

<style scoped>
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.animate-fadeIn {
  animation: fadeIn 0.5s ease forwards;
}
</style>
