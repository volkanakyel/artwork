<template>
  <div
    class="fixed top-0 left-[-80%] w-4/5 h-full bg-white z-[100] p-5 transition-transform duration-300 ease-[cubic-bezier(0.16,1,0.3,1)] shadow-md"
    :class="{ 'transform translate-x-[100%]': isOpen }"
  >
    <div class="flex justify-between items-center mb-8">
      <h2 class="text-2xl font-semibold">Menu</h2>
      <button
        class="bg-transparent border-0 cursor-pointer text-black"
        @click="close"
      >
        <XIcon />
      </button>
    </div>
    <div class="sidebar-content">
      <div
        v-for="(item, index) in menuItems"
        :key="index"
        class="flex items-center py-4 border-b border-gray-100 cursor-pointer hover:bg-gray-50 transition-colors duration-200 opacity-0"
        :class="{ 'animate-slideIn': isOpen }"
        :style="`animation-delay: ${index * 0.1}s`"
      >
        <component
          :is="item.icon"
          class="mr-4"
        />
        <span>{{ item.title }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import {
  BarChart as BarChartIcon,
  Home as HomeIcon,
  Settings as SettingsIcon,
  ShoppingBag as ShoppingBagIcon,
  Users as UsersIcon,
  X as XIcon,
} from 'lucide-vue-next'

defineProps({
  isOpen: {
    type: Boolean,
    default: false,
  },
})

const emit = defineEmits(['close'])

const close = () => {
  emit('close')
}

const menuItems = [
  { title: 'Home', icon: HomeIcon },
  { title: 'Artists', icon: UsersIcon },
  { title: 'Marketplace', icon: ShoppingBagIcon },
  { title: 'Analytics', icon: BarChartIcon },
  { title: 'Settings', icon: SettingsIcon },
]
</script>

<style scoped>
@keyframes slideIn {
  from {
    transform: translateX(-20px);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.animate-slideIn {
  animation: slideIn 0.3s ease forwards;
}
</style>
