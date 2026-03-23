<script setup>
import { ref } from 'vue';
const isSidebarOpen = ref(false);
</script>

<template>
  <div class="friend-container">
    <div class="sidebar-overlay" v-if="isSidebarOpen" @click="isSidebarOpen = false"></div>
    <div class="sidebar" :class="{ 'is-open': isSidebarOpen }">
      <div class="sidebar-content">
        <ul class="menu-group top-group">
          <li @click="isSidebarOpen = false">マイページ</li>
          <li @click="$router.push('/friend'); isSidebarOpen = false">フレンド</li>
          <li @click="isSidebarOpen = false">お知らせ</li>
          <li @click="isSidebarOpen = false">履歴</li>
        </ul>
        <ul class="menu-group middle-group">
          <li @click="isSidebarOpen = false">新規イベント作成/参加</li>
          <li @click="isSidebarOpen = false">進行中のイベント</li>
          <li @click="$router.push('/payment'); isSidebarOpen = false">お金のお支払い</li>
        </ul>
        <div class="sidebar-footer">
          <p class="back-home" @click="$router.push('/'); isSidebarOpen = false">ホームへ戻る</p>
        </div>
      </div>
    </div>

    <header class="header">
      <div class="user-icon-container">
        <div class="user-circle"></div>
        <span class="user-name">名前</span>
      </div>
      <h1 class="app-title">アプリ名</h1>
      <div class="header-icons">
        <div class="icon-black"></div>
        <div class="icon-black menu-trigger" @click="isSidebarOpen = true"></div>
      </div>
    </header>

    <main class="content">
      <button class="add-friend-main-button">友達を追加する</button>
      <div class="request-section">
        <p class="request-alert">❗ 友達申請が届いています</p>
        <div class="request-card">
          <div class="request-avatar blue-avatar"></div>
          <span class="request-name">名前</span>
          <button class="approve-button">承認</button>
        </div>
      </div>
      <h2 class="list-title">友達リスト</h2>
      <div class="friend-list">
        <div class="friend-card" v-for="(color, index) in ['#ff9980', '#ffee10', '#ff0000', '#889900', '#776666']" :key="index">
          <div class="friend-avatar" :style="{ backgroundColor: color }"></div>
          <span class="friend-name-text">名前</span>
        </div>
      </div>
    </main>

    <nav class="bottom-nav">
      <div class="nav-item" @click="$router.push('/')">🏠<br>ホーム</div>
      <div class="nav-item" @click="$router.push('/payment')">💳<br>支払い</div>
      <div class="nav-item active">👥<br>フレンド＆精算</div>
    </nav>
  </div>
</template>

<style scoped>
/* サイドバースタイル */
.sidebar-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.4); z-index: 1000; }
.sidebar { position: fixed; top: 0; right: -75%; width: 75%; height: 100%; background: rgba(0, 0, 0, 0.85); z-index: 1001; transition: right 0.3s ease; padding: 60px 30px; box-sizing: border-box; color: white; }
.sidebar.is-open { right: 0; }
.sidebar-content { display: flex; flex-direction: column; height: 100%; text-align: left; }
.menu-group { list-style: none; padding: 0; margin: 0; }
.top-group { margin-bottom: 40px; }
.middle-group { margin-bottom: auto; }
.menu-group li { font-size: 20px; font-weight: bold; padding: 15px 0; cursor: pointer; }
.sidebar-footer { padding-bottom: 40px; text-align: center; }
.back-home { font-size: 18px; font-weight: bold; cursor: pointer; color: #aaa; }

/* ヘッダー共通 */
.header { display: flex; justify-content: space-between; align-items: center; padding: 0 20px; background-color: #d9d9d9; height: 90px; box-sizing: border-box; }
.user-icon-container { width: 60px; text-align: center; }
.user-circle { width: 45px; height: 45px; background-color: #e3a8a8; border-radius: 50%; margin: 0 auto; }
.user-name { font-size: 12px; display: block; margin-top: 4px; }
.app-title { font-size: 28px; font-weight: bold; flex: 1; text-align: center; margin: 0; }
.header-icons { display: flex; gap: 8px; width: 60px; justify-content: flex-end; }
.icon-black { width: 30px; height: 30px; background-color: black; border-radius: 50%; cursor: pointer; }

/* Friend固有 */
.friend-container { min-height: 100vh; background-color: #eef7ff; padding-bottom: 100px; }
.content { padding: 20px; }
.add-friend-main-button { width: 100%; padding: 12px; background-color: #2169a3; color: white; border: none; border-radius: 25px; font-size: 18px; font-weight: bold; margin-bottom: 25px; }
.request-alert { font-weight: bold; font-size: 18px; margin-bottom: 10px; }
.request-card { background-color: white; display: flex; align-items: center; padding: 10px 20px; border-radius: 40px; margin-bottom: 25px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
.blue-avatar { background-color: #8bb4ff; width: 35px; height: 35px; border-radius: 50%; margin-right: 15px; }
.request-name { flex: 1; font-size: 18px; font-weight: bold; }
.approve-button { background-color: #ffedb3; border: none; padding: 8px 30px; border-radius: 20px; font-weight: bold; }
.list-title { font-size: 20px; font-weight: bold; margin-bottom: 15px; }
.friend-card { background-color: white; display: flex; align-items: center; padding: 12px 25px; border-radius: 50px; margin-bottom: 12px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
.friend-avatar { width: 45px; height: 45px; border-radius: 50%; margin-right: 20px; }
.friend-name-text { font-size: 24px; font-weight: bold; }

/* ナビ共通 */
.bottom-nav { position: fixed; bottom: 0; left: 0; width: 100%; height: 85px; background-color: white; display: flex; justify-content: space-around; align-items: center; border-top: 1px solid #ddd; border-radius: 25px 25px 0 0; z-index: 100; }
.nav-item { text-align: center; font-size: 12px; color: #333; cursor: pointer; font-weight: bold; }
.nav-item.active { color: #3b82f6; }
</style>