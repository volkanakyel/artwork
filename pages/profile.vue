<template>
  <div class="profile-page">
    <!-- Header -->
    <header class="profile-header">
      <button
        class="back-button"
        @click="goToHome"
      >
        <ArrowLeftIcon />
      </button>
      <h1>YOUR ACTIVITY</h1>
    </header>

    <!-- Profile Section -->
    <div class="profile-section">
      <div class="profile-info">
        <div class="profile-avatar">
          <img
            src="https://randomuser.me/api/portraits/women/44.jpg"
            alt="Esther Howard"
          />
        </div>
        <div class="profile-details">
          <h2>Esther Howard</h2>
          <p>Modern art</p>
        </div>
      </div>
      <button class="add-button">
        <PlusIcon />
      </button>
    </div>

    <!-- Featured Artwork -->
    <div class="featured-artwork">
      <div class="artwork-image">
        <img
          src="https://hebbkx1anhila5yf.public.blob.vercel-storage.com/Screenshot%202025-03-06%20at%2015.40.18-ZWqSwAIDdkg5F4rT9Cp2tfIw7MmNiC.png"
          alt="Yellow Abstract Art"
        />
      </div>
      <div class="artwork-info">
        <div class="artwork-price">89.960 ETH</div>
        <div class="artwork-collection">
          <span>Zain Franci Collection</span>
          <div class="collection-avatar">
            <img
              src="https://randomuser.me/api/portraits/men/32.jpg"
              alt="Zain"
            />
          </div>
        </div>
      </div>
    </div>

    <!-- Last Artworks Section -->
    <div class="last-artworks">
      <div class="section-header">
        <h3>LAST ARTWORKS</h3>
        <button class="view-all">View all</button>
      </div>

      <div class="artwork-list">
        <div
          v-for="item in lastArtworks"
          :key="item.title"
          class="artwork-item"
        >
          <div class="item-icon">
            <CircleDollarSignIcon />
          </div>
          <div class="item-info">
            <div class="item-title">{{ item.title }}</div>
            <div class="item-count">{{ item.count }} items</div>
          </div>
          <div class="item-arrow">
            <TrendingUpIcon />
          </div>
        </div>
      </div>
    </div>

    <BottomNav />
  </div>
</template>

<script setup>
import { inject } from 'vue'
import {
  ArrowLeft as ArrowLeftIcon,
  Plus as PlusIcon,
  CircleDollarSign as CircleDollarSignIcon,
  TrendingUp as TrendingUpIcon,
} from 'lucide-vue-next'
import BottomNav from '../components/BottomNav.vue'

// Get shared functionality from parent
const goToHome = inject('goToHome')

const lastArtworks = [
  { title: 'Introductions', count: 2 },
  { title: 'Tiana Gallery', count: 3 },
  { title: 'Aspen Westervelt', count: 6 },
]
</script>

<style scoped>
.profile-page {
  position: relative;
  width: 100%;
  max-width: 430px;
  height: 100vh;
  margin: 0 auto;
  background-color: #f2f2f2;
  overflow-y: auto;
  padding: 20px;
  padding-bottom: 80px;
}

.profile-header {
  display: flex;
  align-items: center;
  margin-bottom: 30px;
}

.back-button {
  background: none;
  border: none;
  padding: 8px;
  margin-right: 15px;
  cursor: pointer;
  color: #000;
}

.profile-header h1 {
  font-size: 22px;
  font-weight: 700;
  letter-spacing: 0.5px;
}

.profile-section {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 30px;
  animation: fadeIn 0.5s ease forwards;
}

.profile-info {
  display: flex;
  align-items: center;
  gap: 15px;
}

.profile-avatar {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  overflow: hidden;
}

.profile-avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.profile-details h2 {
  font-size: 18px;
  font-weight: 600;
  margin-bottom: 4px;
}

.profile-details p {
  font-size: 14px;
  color: #666;
}

.add-button {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background-color: #0f1420;
  color: #fff;
  border: none;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: transform 0.2s ease;
}

.add-button:hover {
  transform: scale(1.05);
}

.featured-artwork {
  background: #fff;
  border-radius: 20px;
  overflow: hidden;
  margin-bottom: 30px;
  animation: fadeIn 0.5s ease forwards;
  animation-delay: 0.1s;
}

.artwork-image {
  width: 100%;
  height: 200px;
  overflow: hidden;
}

.artwork-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.artwork-info {
  padding: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.artwork-price {
  font-size: 20px;
  font-weight: 700;
}

.artwork-collection {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 14px;
  color: #666;
}

.collection-avatar {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  overflow: hidden;
}

.collection-avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.last-artworks {
  animation: slideUp 0.5s ease forwards;
  animation-delay: 0.2s;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.section-header h3 {
  font-size: 18px;
  font-weight: 700;
  letter-spacing: 0.5px;
}

.view-all {
  background: none;
  border: none;
  color: #666;
  font-size: 14px;
  cursor: pointer;
}

.artwork-list {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.artwork-item {
  display: flex;
  align-items: center;
  background: #fff;
  padding: 15px;
  border-radius: 15px;
  animation: slideIn 0.3s ease forwards;
  opacity: 0;
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.artwork-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

.artwork-item:nth-child(1) {
  animation-delay: 0.3s;
}
.artwork-item:nth-child(2) {
  animation-delay: 0.4s;
}
.artwork-item:nth-child(3) {
  animation-delay: 0.5s;
}

.item-icon {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: #f8f8f8;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 15px;
}

.item-info {
  flex: 1;
}

.item-title {
  font-size: 16px;
  font-weight: 600;
  margin-bottom: 4px;
}

.item-count {
  font-size: 14px;
  color: #666;
}

.item-arrow {
  color: #666;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slideUp {
  from {
    transform: translateY(20px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
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
</style>
