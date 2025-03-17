<template>
  <div
    class="relative w-full max-w-[430px] h-screen mx-auto bg-[#f2f2f2] overflow-hidden"
    :class="{ 'menu-open': isMenuOpen }"
  >
    <!-- Use the Sidebar Menu Component -->
    <SidebarMenu
      :is-open="isMenuOpen"
      @close="toggleMenu"
    />

    <!-- Search Overlay -->
    <div
      v-if="isSearchActive"
      class="fixed top-0 left-0 w-full h-full bg-black/50 z-[200] flex justify-center items-start animate-fadeIn"
      @click="closeSearch"
    >
      <div
        class="w-full max-w-[430px] bg-[#f2f2f2] rounded-b-[20px] overflow-hidden animate-slideDown"
        @click.stop
      >
        <div class="flex items-center bg-white p-4 shadow-sm">
          <input
            ref="searchInput"
            v-model="searchQuery"
            type="text"
            class="flex-1 border-none outline-none text-base py-2.5 bg-transparent"
            placeholder="Search artists, artworks..."
            @keyup.esc="closeSearch"
          />
          <button
            class="bg-transparent border-0 cursor-pointer text-gray-500 ml-2.5"
            @click="closeSearch"
          >
            <XIcon size="18" />
          </button>
        </div>
        <div
          v-if="searchQuery.length > 0"
          class="max-h-[60vh] overflow-y-auto py-2.5"
        >
          <div
            v-for="(result, index) in searchResults"
            :key="index"
            class="flex items-center p-4 border-b border-gray-200 bg-white cursor-pointer hover:bg-gray-50 transition-colors animate-scaleUp"
          >
            <div
              class="w-10 h-10 rounded-full bg-gray-100 flex justify-center items-center mr-4 overflow-hidden"
            >
              <img
                v-if="result.type === 'artist'"
                :src="result.image"
                alt="Artist"
                class="w-full h-full object-cover"
              />
              <PaletteIcon
                v-else-if="result.type === 'artwork'"
                size="18"
              />
            </div>
            <div class="flex-1">
              <div class="text-sm font-semibold mb-0.5">{{ result.title }}</div>
              <div class="text-xs text-gray-500">{{ result.subtitle }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Main Content -->
    <div
      class="relative w-full h-full transition-transform duration-300 ease-[cubic-bezier(0.16,1,0.3,1)] p-5 pb-20"
    >
      <!-- Header -->
      <header class="flex justify-center items-center relative mb-8">
        <button
          class="absolute left-0 bg-transparent border-0 cursor-pointer"
          @click="toggleMenu"
        >
          <MenuIcon />
        </button>
        <h1 class="text-[22px] font-bold tracking-wider">BEST ARTISTS</h1>
      </header>

      <!-- Artists Section -->
      <div class="flex gap-5 mb-10 overflow-x-auto pb-2.5 no-scrollbar">
        <div class="flex flex-col items-center gap-2">
          <div
            class="w-[70px] h-[70px] rounded-full overflow-hidden flex justify-center items-center bg-[#0f1420] text-[#ffd700] cursor-pointer transition-all duration-200 hover:scale-105 hover:shadow-md active:scale-95"
            @click="activateSearch"
          >
            <SearchIcon class="w-6 h-6" />
          </div>
        </div>
        <div
          v-for="artist in artists"
          :key="artist.name"
          class="flex flex-col items-center gap-2 animate-fadeIn"
          :style="`animation-delay: ${artists.indexOf(artist) * 0.1}s`"
        >
          <div class="w-[70px] h-[70px] rounded-full overflow-hidden">
            <img
              :src="artist.avatar"
              :alt="artist.name"
              class="w-full h-full object-cover"
            />
          </div>
          <div class="text-sm font-medium">{{ artist.name }}</div>
        </div>
      </div>

      <!-- Financial Section -->
      <div class="mb-8">
        <h2 class="text-2xl font-bold mb-5">DEC 2024</h2>

        <div
          class="flex items-center mb-4 animate-slideIn"
          :style="`animation-delay: 0s`"
        >
          <div class="w-10 h-10 rounded-full flex justify-center items-center mr-4 bg-white">
            <TrendingUpIcon />
          </div>
          <div class="text-base font-medium flex-1">Profit</div>
          <div class="text-base font-semibold">+$2 450</div>
        </div>

        <div
          class="flex items-center mb-4 animate-slideIn"
          :style="`animation-delay: 0.1s`"
        >
          <div class="w-10 h-10 rounded-full flex justify-center items-center mr-4 bg-white">
            <TrendingDownIcon />
          </div>
          <div class="text-base font-medium flex-1">Spending</div>
          <div class="text-base font-semibold">-$1 280</div>
        </div>

        <div
          class="flex items-center mb-4 animate-slideIn"
          :style="`animation-delay: 0.2s`"
        >
          <div class="w-10 h-10 rounded-full flex justify-center items-center mr-4 bg-white">
            <DollarSignIcon />
          </div>
          <div class="text-base font-medium flex-1">Balance</div>
          <div class="text-base font-semibold">+$12 650</div>
        </div>
      </div>

      <!-- Art Items -->
      <div class="mb-20">
        <ArtItem
          v-for="item in artItems"
          :key="item.title"
          :item="item"
        />
      </div>

      <BottomNav />
    </div>
  </div>
</template>

<script setup>
import {
  DollarSign as DollarSignIcon,
  Menu as MenuIcon,
  Palette as PaletteIcon,
  Search as SearchIcon,
  TrendingDown as TrendingDownIcon,
  TrendingUp as TrendingUpIcon,
  X as XIcon,
} from 'lucide-vue-next'
import { computed, nextTick, ref } from 'vue'
import ArtItem from '../components/Art/ArtItem'
import BottomNav from '../components/BottomNav.vue'
import SidebarMenu from '../components/SidebarMenu.vue'

const isMenuOpen = ref(false)
const isSearchActive = ref(false)
const searchQuery = ref('')
const searchInput = ref(null)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const activateSearch = async () => {
  isSearchActive.value = true
  // Focus the input after the animation completes
  await nextTick()
  searchInput.value?.focus()
}

const closeSearch = () => {
  isSearchActive.value = false
  searchQuery.value = ''
}

const artists = ref([
  {
    name: 'Zain',
    avatar: 'https://randomuser.me/api/portraits/men/32.jpg',
  },
  {
    name: 'Kierra',
    avatar: 'https://randomuser.me/api/portraits/women/44.jpg',
  },
  {
    name: 'Jordyn',
    avatar: 'https://randomuser.me/api/portraits/women/68.jpg',
  },
])

const artItems = ref([
  {
    title: 'Madelyn Grace Art',
    description: "Kota Ezawa's Flat, Stylized Paintings",
    price: '0.260 ETH',
    image:
      'https://hebbkx1anhila5yf.public.blob.vercel-storage.com/Screenshot%202025-03-06%20at%2015.29.56-OhGWfoj6vKTZDVqXUtZeDQqT5mrkN4.png',
  },
  {
    title: 'Wilson Korsgaard',
    description: 'Gallerist Emi Eu Is Asian Art in Singapore',
    price: '0.830 ETH',
    image:
      'https://hebbkx1anhila5yf.public.blob.vercel-storage.com/Screenshot%202025-03-06%20at%2015.29.56-OhGWfoj6vKTZDVqXUtZeDQqT5mrkN4.png',
  },
])

// Mock search results based on query
const searchResults = computed(() => {
  if (!searchQuery.value) return []

  const query = searchQuery.value.toLowerCase()
  const results = []

  // Search artists
  artists.value.forEach(artist => {
    if (artist.name.toLowerCase().includes(query)) {
      results.push({
        type: 'artist',
        title: artist.name,
        subtitle: 'Artist',
        image: artist.avatar,
      })
    }
  })

  // Search artworks
  artItems.value.forEach(item => {
    if (
      item.title.toLowerCase().includes(query) ||
      item.description.toLowerCase().includes(query)
    ) {
      results.push({
        type: 'artwork',
        title: item.title,
        subtitle: item.description,
        image: item.image,
      })
    }
  })

  return results
})
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Inter', sans-serif;
}

/* Menu open effect for main content */
.menu-open .main-content {
  transform: translateX(80%);
  border-radius: 20px;
  overflow: hidden;
  box-shadow: -5px 0 25px rgba(0, 0, 0, 0.1);
}

/* Hide scrollbar for Chrome, Safari and Opera */
.no-scrollbar::-webkit-scrollbar {
  display: none;
}

/* Animations */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

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

@keyframes slideDown {
  from {
    transform: translateY(-100%);
  }
  to {
    transform: translateY(0);
  }
}

@keyframes scaleUp {
  from {
    transform: scale(0.8);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

.animate-fadeIn {
  animation: fadeIn 0.5s ease forwards;
}

.animate-slideIn {
  animation: slideIn 0.3s ease forwards;
}

.animate-slideDown {
  animation: slideDown 0.3s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

.animate-scaleUp {
  animation: scaleUp 0.2s ease forwards;
}
</style>
