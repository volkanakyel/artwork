<template>
  <div
    class="app-container"
    :class="{ 'menu-open': isMenuOpen }"
  >
    <!-- Sidebar Menu -->
    <div
      class="sidebar-menu"
      :class="{ open: isMenuOpen }"
    >
      <div class="sidebar-header">
        <h2>Menu</h2>
        <button
          class="close-btn"
          @click="toggleMenu"
        >
          <XIcon />
        </button>
      </div>
      <div class="sidebar-content">
        <div class="menu-item">
          <HomeIcon class="menu-icon" />
          <span>Home</span>
        </div>
        <div class="menu-item">
          <UsersIcon class="menu-icon" />
          <span>Artists</span>
        </div>
        <div class="menu-item">
          <ShoppingBagIcon class="menu-icon" />
          <span>Marketplace</span>
        </div>
        <div class="menu-item">
          <BarChartIcon class="menu-icon" />
          <span>Analytics</span>
        </div>
        <div class="menu-item">
          <SettingsIcon class="menu-icon" />
          <span>Settings</span>
        </div>
      </div>
    </div>

    <!-- Search Overlay -->
    <div
      v-if="isSearchActive"
      class="search-overlay"
      @click="closeSearch"
    >
      <div
        class="search-container"
        @click.stop
      >
        <div class="search-input-container">
          <input
            ref="searchInput"
            v-model="searchQuery"
            type="text"
            class="search-input"
            placeholder="Search artists, artworks..."
            @keyup.esc="closeSearch"
          />
          <button
            class="search-close-btn"
            @click="closeSearch"
          >
            <XIcon size="18" />
          </button>
        </div>
        <div
          v-if="searchQuery.length > 0"
          class="search-results"
        >
          <div
            v-for="(result, index) in searchResults"
            :key="index"
            class="search-result-item"
          >
            <div class="result-icon">
              <img
                v-if="result.type === 'artist'"
                :src="result.image"
                alt="Artist"
                class="result-image"
              />
              <PaletteIcon
                v-else-if="result.type === 'artwork'"
                size="18"
              />
            </div>
            <div class="result-details">
              <div class="result-title">{{ result.title }}</div>
              <div class="result-subtitle">{{ result.subtitle }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Main Content -->
    <div class="main-content">
      <!-- Header -->
      <header class="app-header">
        <button
          class="menu-btn"
          @click="toggleMenu"
        >
          <MenuIcon />
        </button>
        <h1>BEST ARTISTS</h1>
      </header>

      <!-- Artists Section -->
      <div class="artists-section">
        <div class="artist-item search">
          <div
            class="artist-avatar search-icon"
            @click="activateSearch"
          >
            <SearchIcon class="icon" />
          </div>
        </div>
        <div
          v-for="artist in artists"
          :key="artist.name"
          class="artist-item"
        >
          <div class="artist-avatar">
            <img
              :src="artist.avatar"
              :alt="artist.name"
            />
          </div>
          <div class="artist-name">{{ artist.name }}</div>
        </div>
      </div>

      <!-- Financial Section -->
      <div class="financial-section">
        <h2>DEC 2024</h2>

        <div class="financial-item">
          <div class="financial-icon profit">
            <TrendingUpIcon />
          </div>
          <div class="financial-label">Profit</div>
          <div class="financial-value positive">+$2 450</div>
        </div>

        <div class="financial-item">
          <div class="financial-icon spending">
            <TrendingDownIcon />
          </div>
          <div class="financial-label">Spending</div>
          <div class="financial-value negative">-$1 280</div>
        </div>

        <div class="financial-item">
          <div class="financial-icon balance">
            <DollarSignIcon />
          </div>
          <div class="financial-label">Balance</div>
          <div class="financial-value positive">+$12 650</div>
        </div>
      </div>

      <!-- Art Items -->
      <div class="art-items">
        <div
          v-for="item in artItems"
          :key="item.title"
          class="art-item"
        >
          <div class="art-thumbnail">
            <img
              :src="item.image"
              :alt="item.title"
            />
          </div>
          <div class="art-details">
            <h3>{{ item.title }}</h3>
            <p>{{ item.description }}</p>
            <div class="art-price">{{ item.price }}</div>
          </div>
          <div class="art-arrow">
            <ArrowRightIcon />
          </div>
        </div>
      </div>

      <!-- Bottom Navigation -->
      <div class="bottom-nav">
        <div class="nav-item active">
          <div class="nav-icon">
            <LayoutGridIcon />
          </div>
          <div class="nav-label">Home</div>
        </div>
        <div class="nav-item">
          <div class="nav-icon">
            <BellIcon />
          </div>
        </div>
        <div class="nav-item">
          <div class="nav-icon">
            <CameraIcon />
          </div>
        </div>
        <div class="nav-item">
          <div class="nav-icon">
            <UserIcon />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import {
  ArrowRight as ArrowRightIcon,
  BarChart as BarChartIcon,
  Bell as BellIcon,
  Camera as CameraIcon,
  DollarSign as DollarSignIcon,
  Home as HomeIcon,
  LayoutGrid as LayoutGridIcon,
  Menu as MenuIcon,
  Palette as PaletteIcon,
  Search as SearchIcon,
  Settings as SettingsIcon,
  ShoppingBag as ShoppingBagIcon,
  TrendingDown as TrendingDownIcon,
  TrendingUp as TrendingUpIcon,
  User as UserIcon,
  Users as UsersIcon,
  X as XIcon,
} from 'lucide-vue-next'
import { computed, nextTick, ref } from 'vue'

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

.app-container {
  position: relative;
  width: 100%;
  max-width: 430px;
  height: 100vh;
  margin: 0 auto;
  background-color: #f2f2f2;
  overflow: hidden;
}

/* Sidebar Menu */
.sidebar-menu {
  position: fixed;
  top: 0;
  left: -80%;
  width: 80%;
  height: 100%;
  background-color: #fff;
  z-index: 100;
  padding: 20px;
  transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
}

.sidebar-menu.open {
  transform: translateX(100%);
}

.sidebar-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 30px;
}

.sidebar-header h2 {
  font-size: 24px;
  font-weight: 600;
}

.close-btn {
  background: none;
  border: none;
  cursor: pointer;
  color: #000;
}

.menu-item {
  display: flex;
  align-items: center;
  padding: 15px 0;
  border-bottom: 1px solid #f0f0f0;
}

.menu-icon {
  margin-right: 15px;
}

/* Search Overlay */
.search-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 200;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  animation: fadeIn 0.2s ease forwards;
}

.search-container {
  width: 100%;
  max-width: 430px;
  background-color: #f2f2f2;
  border-radius: 0 0 20px 20px;
  overflow: hidden;
  animation: slideDown 0.3s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

.search-input-container {
  display: flex;
  align-items: center;
  background-color: #fff;
  padding: 15px 20px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
}

.search-input {
  flex: 1;
  border: none;
  outline: none;
  font-size: 16px;
  padding: 10px 0;
  background: transparent;
}

.search-close-btn {
  background: none;
  border: none;
  cursor: pointer;
  color: #666;
  margin-left: 10px;
}

.search-results {
  max-height: 60vh;
  overflow-y: auto;
  padding: 10px 0;
}

.search-result-item {
  display: flex;
  align-items: center;
  padding: 15px 20px;
  border-bottom: 1px solid #eee;
  background-color: #fff;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.search-result-item:hover {
  background-color: #f9f9f9;
}

.result-icon {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background-color: #f0f0f0;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-right: 15px;
  overflow: hidden;
}

.result-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.result-details {
  flex: 1;
}

.result-title {
  font-size: 14px;
  font-weight: 600;
  margin-bottom: 3px;
}

.result-subtitle {
  font-size: 12px;
  color: #666;
}

/* Main Content */
.main-content {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  padding: 20px;
  padding-bottom: 80px;
}

.menu-open .main-content {
  transform: translateX(80%);
  border-radius: 20px;
  overflow: hidden;
  box-shadow: -5px 0 25px rgba(0, 0, 0, 0.1);
}

/* Header */
.app-header {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  margin-bottom: 30px;
}

.app-header h1 {
  font-size: 22px;
  font-weight: 700;
  letter-spacing: 0.5px;
}

.menu-btn {
  position: absolute;
  left: 0;
  background: none;
  border: none;
  cursor: pointer;
}

/* Artists Section */
.artists-section {
  display: flex;
  gap: 20px;
  margin-bottom: 40px;
  overflow-x: auto;
  padding-bottom: 10px;
}

.artists-section::-webkit-scrollbar {
  display: none;
}

.artist-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
}

.artist-avatar {
  width: 70px;
  height: 70px;
  border-radius: 50%;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

.artist-avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.search-icon {
  background-color: #0f1420;
  color: #ffd700;
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.search-icon:hover {
  transform: scale(1.05);
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

.search-icon:active {
  transform: scale(0.95);
}

.icon {
  width: 24px;
  height: 24px;
}

.artist-name {
  font-size: 14px;
  font-weight: 500;
}

/* Financial Section */
.financial-section {
  margin-bottom: 30px;
}

.financial-section h2 {
  font-size: 24px;
  font-weight: 700;
  margin-bottom: 20px;
}

.financial-item {
  display: flex;
  align-items: center;
  margin-bottom: 15px;
}

.financial-icon {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-right: 15px;
  background-color: #fff;
}

.financial-label {
  font-size: 16px;
  font-weight: 500;
  flex: 1;
}

.financial-value {
  font-size: 16px;
  font-weight: 600;
}

.positive {
  color: #000;
}

.negative {
  color: #000;
}

/* Art Items */
.art-items {
  margin-bottom: 80px;
}

.art-item {
  display: flex;
  align-items: center;
  background-color: #fff;
  border-radius: 15px;
  padding: 15px;
  margin-bottom: 15px;
}

.art-thumbnail {
  width: 60px;
  height: 60px;
  border-radius: 10px;
  overflow: hidden;
  margin-right: 15px;
}

.art-thumbnail img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.art-details {
  flex: 1;
}

.art-details h3 {
  font-size: 16px;
  font-weight: 600;
  margin-bottom: 5px;
}

.art-details p {
  font-size: 12px;
  color: #666;
  margin-bottom: 5px;
}

.art-price {
  font-size: 14px;
  font-weight: 600;
}

.art-arrow {
  margin-left: 10px;
}

/* Bottom Navigation */
.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 0;
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
}

.nav-item.active {
  background-color: #ffd700;
  color: #0f1420;
  padding: 8px 20px;
  border-radius: 20px;
}

.nav-icon {
  display: flex;
  justify-content: center;
  align-items: center;
}

.nav-label {
  font-size: 12px;
  margin-top: 4px;
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

.art-item {
  animation: fadeIn 0.5s ease forwards;
}

.financial-item {
  animation: slideIn 0.3s ease forwards;
}

.financial-item:nth-child(2) {
  animation-delay: 0.1s;
}

.financial-item:nth-child(3) {
  animation-delay: 0.2s;
}

.artist-item {
  animation: fadeIn 0.5s ease forwards;
}

.artist-item:nth-child(2) {
  animation-delay: 0.1s;
}

.artist-item:nth-child(3) {
  animation-delay: 0.2s;
}

.artist-item:nth-child(4) {
  animation-delay: 0.3s;
}

.search-result-item {
  animation: scaleUp 0.2s ease forwards;
}

/* Hover effects */
.art-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.menu-item:hover {
  background-color: #f9f9f9;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

/* Sidebar animation */
.sidebar-menu {
  transform: translateX(0);
}

.sidebar-menu.open .menu-item {
  opacity: 0;
  animation: slideIn 0.3s ease forwards;
}

.sidebar-menu.open .menu-item:nth-child(1) {
  animation-delay: 0.1s;
}

.sidebar-menu.open .menu-item:nth-child(2) {
  animation-delay: 0.2s;
}

.sidebar-menu.open .menu-item:nth-child(3) {
  animation-delay: 0.3s;
}

.sidebar-menu.open .menu-item:nth-child(4) {
  animation-delay: 0.4s;
}

.sidebar-menu.open .menu-item:nth-child(5) {
  animation-delay: 0.5s;
}
</style>
