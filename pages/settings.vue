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
      <h1>SETTINGS</h1>
    </header>

    <!-- User Profile Section -->
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
          <p>esther@artwork.com</p>
        </div>
      </div>
      <button class="edit-button">
        <PencilIcon size="18" />
      </button>
    </div>

    <!-- Settings Sections -->
    <div class="settings-group">
      <h3>Account</h3>
      <div class="settings-list">
        <div class="settings-item">
          <div class="settings-icon account">
            <UserIcon />
          </div>
          <div class="settings-info">
            <div class="settings-title">Personal Information</div>
            <div class="settings-subtitle">Update your personal details</div>
          </div>
          <ChevronRightIcon />
        </div>

        <div class="settings-item">
          <div class="settings-icon security">
            <ShieldIcon />
          </div>
          <div class="settings-info">
            <div class="settings-title">Security</div>
            <div class="settings-subtitle">Password and authentication</div>
          </div>
          <ChevronRightIcon />
        </div>

        <div class="settings-item">
          <div class="settings-icon wallet">
            <WalletIcon />
          </div>
          <div class="settings-info">
            <div class="settings-title">Payment Methods</div>
            <div class="settings-subtitle">Connected cards and wallets</div>
          </div>
          <ChevronRightIcon />
        </div>
      </div>
    </div>

    <div class="settings-group">
      <h3>Preferences</h3>
      <div class="settings-list">
        <div class="settings-item">
          <div class="settings-icon notifications">
            <BellIcon />
          </div>
          <div class="settings-info">
            <div class="settings-title">Notifications</div>
            <div class="settings-subtitle">Manage notification preferences</div>
          </div>
          <ChevronRightIcon />
        </div>

        <div class="settings-item">
          <div class="settings-icon appearance">
            <PaletteIcon />
          </div>
          <div class="settings-info">
            <div class="settings-title">Appearance</div>
            <div class="settings-subtitle">Dark mode and theme options</div>
          </div>
          <ChevronRightIcon />
        </div>

        <div class="settings-item">
          <div class="settings-icon language">
            <GlobeIcon />
          </div>
          <div class="settings-info">
            <div class="settings-title">Language</div>
            <div class="settings-subtitle">Change language preferences</div>
          </div>
          <ChevronRightIcon />
        </div>
      </div>
    </div>

    <div class="settings-group">
      <h3>Other</h3>
      <div class="settings-list">
        <div class="settings-item">
          <div class="settings-icon help">
            <HelpCircleIcon />
          </div>
          <div class="settings-info">
            <div class="settings-title">Help & Support</div>
            <div class="settings-subtitle">FAQs and contact support</div>
          </div>
          <ChevronRightIcon />
        </div>

        <div class="settings-item danger">
          <div class="settings-icon logout">
            <LogOutIcon />
          </div>
          <div class="settings-info">
            <div class="settings-title">Log Out</div>
          </div>
          <ChevronRightIcon />
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
  Bell as BellIcon,
  ChevronRight as ChevronRightIcon,
  Globe as GlobeIcon,
  HelpCircle as HelpCircleIcon,
  LogOut as LogOutIcon,
  Palette as PaletteIcon,
  Pencil as PencilIcon,
  Shield as ShieldIcon,
  User as UserIcon,
  Wallet as WalletIcon,
} from 'lucide-vue-next'

const goToHome = inject('goToHome')
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

.edit-button {
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

.edit-button:hover {
  transform: scale(1.05);
}

.settings-group {
  margin-bottom: 30px;
  animation: slideUp 0.5s ease forwards;
}

.settings-group h3 {
  font-size: 16px;
  font-weight: 600;
  margin-bottom: 15px;
  color: #666;
}

.settings-list {
  background: #fff;
  border-radius: 15px;
  overflow: hidden;
}

.settings-item {
  display: flex;
  align-items: center;
  padding: 15px;
  cursor: pointer;
  transition: all 0.2s ease;
  animation: slideIn 0.3s ease forwards;
  opacity: 0;
}

.settings-item:not(:last-child) {
  border-bottom: 1px solid #f0f0f0;
}

.settings-item:hover {
  background-color: #f9f9f9;
}

.settings-icon {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 15px;
}

.settings-icon.account {
  background-color: #e4f1ff;
  color: #4d94ff;
}
.settings-icon.security {
  background-color: #ffe4e4;
  color: #ff4d4d;
}
.settings-icon.wallet {
  background-color: #e4ffe4;
  color: #4dff4d;
}
.settings-icon.notifications {
  background-color: #fff4e4;
  color: #ffd700;
}
.settings-icon.appearance {
  background-color: #f4e4ff;
  color: #9f4dff;
}
.settings-icon.language {
  background-color: #e4fff4;
  color: #4dffd7;
}
.settings-icon.help {
  background-color: #ffe4f4;
  color: #ff4d94;
}
.settings-icon.logout {
  background-color: #ffe4e4;
  color: #ff4d4d;
}

.settings-info {
  flex: 1;
}

.settings-title {
  font-size: 16px;
  font-weight: 500;
  margin-bottom: 2px;
}

.settings-subtitle {
  font-size: 12px;
  color: #666;
}

.danger .settings-title {
  color: #ff4d4d;
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

.settings-item:nth-child(1) {
  animation-delay: 0.1s;
}
.settings-item:nth-child(2) {
  animation-delay: 0.2s;
}
.settings-item:nth-child(3) {
  animation-delay: 0.3s;
}
</style>
