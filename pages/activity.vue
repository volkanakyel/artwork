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
      <h1>NOTIFICATIONS</h1>
    </header>

    <!-- Notifications Section -->
    <div class="notifications-section">
      <div class="section-header">
        <h3>TODAY</h3>
        <button class="view-all">Clear all</button>
      </div>

      <div class="notification-list">
        <div
          v-for="notification in notifications"
          :key="notification.id"
          class="notification-item"
        >
          <div
            class="notification-icon"
            :class="notification.type"
          >
            <component :is="getNotificationIcon(notification.type)" />
          </div>
          <div class="notification-info">
            <div class="notification-title">{{ notification.title }}</div>
            <div class="notification-time">{{ notification.time }}</div>
          </div>
          <div class="notification-arrow">
            <ArrowRightIcon />
          </div>
        </div>
      </div>
    </div>

    <!-- Replace the bottom navigation with the component -->
    <BottomNav />
  </div>
</template>

<script setup>
import { inject } from 'vue'
import {
  ArrowLeft as ArrowLeftIcon,
  ArrowRight as ArrowRightIcon,
  Heart as HeartIcon,
  MessageCircle as MessageCircleIcon,
  Share2 as ShareIcon,
  Star as StarIcon,
} from 'lucide-vue-next'

// Get shared functionality from parent
const goToHome = inject('goToHome')

const notifications = [
  {
    id: 1,
    type: 'like',
    title: 'Jordyn liked your artwork "Abstract Harmony"',
    time: '2 minutes ago',
  },
  {
    id: 2,
    type: 'comment',
    title: 'Kierra commented on your recent post',
    time: '15 minutes ago',
  },
  {
    id: 3,
    type: 'share',
    title: 'Zain shared your artwork with their followers',
    time: '1 hour ago',
  },
  {
    id: 4,
    type: 'favorite',
    title: 'Your artwork was added to favorites',
    time: '2 hours ago',
  },
]

const getNotificationIcon = type => {
  const icons = {
    like: HeartIcon,
    comment: MessageCircleIcon,
    share: ShareIcon,
    favorite: StarIcon,
  }
  return icons[type]
}
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

.notification-list {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.notification-item {
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

.notification-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

.notification-item:nth-child(1) {
  animation-delay: 0.1s;
}
.notification-item:nth-child(2) {
  animation-delay: 0.2s;
}
.notification-item:nth-child(3) {
  animation-delay: 0.3s;
}
.notification-item:nth-child(4) {
  animation-delay: 0.4s;
}

.notification-icon {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 15px;
}

.notification-icon.like {
  background-color: #ffe4e4;
  color: #ff4d4d;
}

.notification-icon.comment {
  background-color: #e4f1ff;
  color: #4d94ff;
}

.notification-icon.share {
  background-color: #e4ffe4;
  color: #4dff4d;
}

.notification-icon.favorite {
  background-color: #fff4e4;
  color: #ffd700;
}

.notification-info {
  flex: 1;
}

.notification-title {
  font-size: 14px;
  font-weight: 500;
  margin-bottom: 4px;
}

.notification-time {
  font-size: 12px;
  color: #666;
}

.notification-arrow {
  color: #666;
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
