<template>
  <div
    class="fixed bottom-0 left-1/2 transform -translate-x-1/2 w-full max-w-[430px] h-[70px] bg-[#0f1420] rounded-t-[20px] flex justify-around items-center px-5 z-10"
  >
    <div
      v-for="item in navItems"
      :key="item.path"
      class="flex flex-col items-center text-white transition-all duration-300"
      :class="{
        'bg-[#ffd700] text-[#0f1420] px-5 py-2 rounded-[20px]': currentRoute === item.path,
      }"
    >
      <div
        class="flex justify-center items-center cursor-pointer transition-transform duration-200 active:scale-90"
        @click="navigateTo(item.path)"
      >
        <component :is="item.icon" />
      </div>
      <div
        v-if="item.label"
        class="text-xs mt-1"
      >
        {{ item.label }}
      </div>
    </div>
  </div>
</template>

<script setup>
import {
  Bell as BellIcon,
  Camera as CameraIcon,
  LayoutGrid as LayoutGridIcon,
  User as UserIcon,
} from 'lucide-vue-next'
import { computed } from 'vue'
import { useRoute, useRouter } from 'vue-router'

const route = useRoute()
const router = useRouter()
const currentRoute = computed(() => route.path)

const navItems = [
  { path: '/', icon: LayoutGridIcon, label: 'Home' },
  { path: '/activity', icon: BellIcon, label: null },
  { path: '/camera', icon: CameraIcon, label: null },
  { path: '/profile', icon: UserIcon, label: null },
]

const navigateTo = async path => {
  if (path === currentRoute.value) return
  await router.push(path)
}
</script>

<style scoped>
.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
  max-width: 430px;
  height: 70px;
  background-color: #0f1420;
  border-radius: 20px 20px 0 0;
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 0 20px;
  z-index: 10;
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #fff;
  transition: color 0.3s ease;
}

.nav-item.active {
  background-color: #ffd700;
  color: #0f1420;
  padding: 8px 20px;
  border-radius: 20px;
  transition: all 0.3s ease;
}

.nav-icon {
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transition: transform 0.2s ease;
}

.nav-icon:active {
  transform: scale(0.9);
}

.nav-label {
  font-size: 12px;
  margin-top: 4px;
}
</style>
