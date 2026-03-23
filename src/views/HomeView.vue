<template>
  <div class="home-container">
    <div class="sidebar-overlay" v-if="isSidebarOpen" @click="isSidebarOpen = false"></div>
    <div class="sidebar" :class="{ 'is-open': isSidebarOpen }">
      <div class="sidebar-content">
        <ul class="menu-group top-group">
          <li @click="isSidebarOpen = false">マイページ</li>
          <li @click="isSidebarOpen = false">フレンド</li>
          <li @click="isSidebarOpen = false">お知らせ</li>
          <li @click="isSidebarOpen = false">履歴</li>
        </ul>

        <ul class="menu-group middle-group">
          <li @click="isSidebarOpen = false">新規イベント作成/参加</li>
          <li @click="isSidebarOpen = false">進行中のイベント</li>
          <li @click="isSidebarOpen = false">お金のお支払い</li>
        </ul>

        <div class="sidebar-footer">
          <p class="back-home" @click="isSidebarOpen = false">ホームへ戻る</p>
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

    <section class="payment-status">
      <h2 class="section-title">お支払い状況</h2>
      <div class="status-card">
        <div class="status-box">
          <span class="badge blue">お支払い待ち</span>
          <div class="price blue-text">料金</div>
          <div class="progress-bar"><div class="bar blue-bar"></div></div>
        </div>
        <div class="divider"></div>
        <div class="status-box">
          <span class="badge orange">未払い</span>
          <div class="price orange-text">料金</div>
          <div class="progress-bar"><div class="bar orange-bar"></div></div>
        </div>
      </div>
    </section>

    <section class="ongoing-events">
      <h2 class="section-title">進行中のイベント</h2>
      <div class="event-list-container">
        <div class="event-item" v-for="i in 3" :key="i">
          <div class="event-tag" :class="{ gray: i > 1 }">イベント{{ i }}</div>
          <div class="event-info">
            <h3 class="event-name">イベント名 {{ i }}</h3>
            <div class="member-icons">
              <span class="circle c1"></span><span class="circle c2"></span><span class="circle c3"></span>
            </div>
          </div>
          <div class="event-amount">合計金額</div>
        </div>
      </div>
    </section>

    <button class="add-button">+</button>

    <nav class="bottom-nav">
        <div class="nav-item active">🏠<br>ホーム</div>
        <div class="nav-item" @click="$router.push('/payment')">💳<br>支払い</div>
        <div class="nav-item" @click="$router.push('/friend')">👥<br>フレンド＆精算</div>
    </nav>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// サイドバーの開閉状態を管理する変数
const isSidebarOpen = ref(false);
</script>

<style scoped>
/* --- サイドバーのスタイル (半透明 & 左揃え) --- */
.sidebar-overlay {
  position: fixed; top: 0; left: 0; width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.4); z-index: 1000;
}

.sidebar {
  position: fixed; top: 0; right: -75%; width: 75%; height: 100%;
  background: rgba(0, 0, 0, 0.85); /* 半透明の黒 */
  z-index: 1001; transition: right 0.3s ease;
  padding: 60px 30px;
  box-sizing: border-box;
  color: white;
}

.sidebar.is-open { right: 0; }

.sidebar-content {
  display: flex;
  flex-direction: column;
  height: 100%;
  text-align: left; /* 左揃え */
}

.menu-group {
  list-style: none;
  padding: 0;
  margin: 0;
}

.top-group { margin-bottom: 40px; }
.middle-group { margin-bottom: auto; }

.menu-group li {
  font-size: 20px;
  font-weight: bold;
  padding: 15px 0;
  cursor: pointer;
}

.sidebar-footer {
  padding-bottom: 40px;
  text-align: center;
}

.back-home {
  font-size: 18px;
  font-weight: bold;
  cursor: pointer;
  color: #aaa;
}

/* ヘッダー共通スタイル */
.header { display: flex; justify-content: space-between; align-items: center; padding: 0 20px; background-color: #d9d9d9; height: 90px; box-sizing: border-box; }
.user-icon-container { width: 60px; text-align: center; }
.user-circle { width: 45px; height: 45px; background-color: #e3a8a8; border-radius: 50%; margin: 0 auto; }
.user-name { font-size: 12px; display: block; margin-top: 4px; }
.app-title { font-size: 28px; font-weight: bold; flex: 1; text-align: center; margin: 0; }
.header-icons { display: flex; gap: 8px; width: 60px; justify-content: flex-end; }
.icon-black { width: 30px; height: 30px; background-color: black; border-radius: 50%; cursor: pointer; }

/* Home固有スタイル */
.home-container { min-height: 100vh; background-color: #f0f4f8; padding-bottom: 100px; position: relative; }
.payment-status { padding: 20px; }
.section-title { font-size: 18px; margin-bottom: 15px; font-weight: bold; }
.status-card { display: flex; background-color: white; border-radius: 20px; padding: 20px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); align-items: center; }
.status-box { text-align: center; flex: 1; }
.badge { display: inline-block; color: white; padding: 2px 12px; border-radius: 10px; font-size: 12px; margin-bottom: 8px; }
.blue { background-color: #3b82f6; }
.orange { background-color: #f59e0b; }
.price { font-size: 24px; font-weight: bold; margin-bottom: 8px; }
.blue-text { color: #3b82f6; }
.orange-text { color: #f59e0b; }
.divider { width: 1px; height: 60px; background-color: #ccc; margin: 0 10px; }
.progress-bar { width: 80%; height: 6px; background-color: #eee; border-radius: 3px; margin: 0 auto; }
.blue-bar { width: 60%; background-color: #3b82f6; height: 100%; border-radius: 3px; }
.orange-bar { width: 40%; background-color: #f59e0b; height: 100%; border-radius: 3px; }
.ongoing-events { padding: 0 20px; }
.event-list-container { background-color: #dcdcdc; padding: 15px; border-radius: 10px; }
.event-item { background-color: white; border-radius: 15px; padding: 12px; margin-bottom: 10px; display: flex; align-items: center; }
.event-tag { background-color: #3b82f6; color: white; font-size: 10px; padding: 8px 4px; border-radius: 8px; width: 50px; text-align: center; margin-right: 12px; }
.event-tag.gray { background-color: #999; }
.event-info { flex: 1; }
.event-name { font-size: 16px; margin: 0 0 4px 0; }
.member-icons { display: flex; gap: 4px; }
.circle { width: 18px; height: 18px; border-radius: 50%; }
.c1 { background-color: #fca5a5; } .c2 { background-color: #93c5fd; } .c3 { background-color: #86efac; }
.event-amount { font-size: 13px; font-weight: bold; }
.add-button { position: fixed; right: 20px; bottom: 100px; width: 60px; height: 60px; background-color: #3b82f6; color: white; border: none; border-radius: 50%; font-size: 40px; box-shadow: 0 4px 10px rgba(0,0,0,0.3); }

/* ナビ共通スタイル */
.bottom-nav { position: fixed; bottom: 0; left: 0; width: 100%; height: 85px; background-color: white; display: flex; justify-content: space-around; align-items: center; border-top: 1px solid #ddd; border-radius: 25px 25px 0 0; z-index: 100; }
.nav-item { text-align: center; font-size: 12px; color: #333; cursor: pointer; font-weight: bold; }
.nav-item.active { color: #3b82f6; }
</style>