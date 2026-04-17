<script setup lang="ts">
import { ref } from 'vue'

const activeTab = ref<'client' | 'admin'>('client')
const modalImage = ref<string | null>(null)
const base = import.meta.env.BASE_URL

const clientImages = [
  { src: base + 'pages_UI_Display_Images/Client01_用户登录首页面.png', title: '01. 用户登录', desc: '系统启动后的首屏，提供清爽的登录入口。', meta: 'Client01_用户登录首页面.png' },
  { src: base + 'pages_UI_Display_Images/Client02_提示刷卡页面.png', title: '02. 刷卡交互提示', desc: '提示用户放置校园卡，模拟 NFC/RFID 硬件交互。', meta: 'Client02_提示刷卡页面.png' },
  { src: base + 'pages_UI_Display_Images/Client03_提示输入账号信息页面.png', title: '03. 账号输入', desc: '当未检测到实体卡时，支持手动输入账号。', meta: 'Client03_提示输入账号信息页面.png' },
  { src: base + 'pages_UI_Display_Images/Client04_首次登录设置密码激活账号页面.png', title: '04. 账号激活', desc: '新用户首次使用需设置密码以激活账号。', meta: 'Client04_首次登录设置密码...' },
  { src: base + 'pages_UI_Display_Images/Client05_非首次登录直接输入密码页面.png', title: '05. 密码验证', desc: '老用户登录时的安全密码校验界面。', meta: 'Client05_非首次登录...' },
  { src: base + 'pages_UI_Display_Images/Client06_重置密码页面.png', title: '06. 密码重置', desc: '提供用户自助式密码更改功能。', meta: 'Client06_重置密码页面.png' },
  { src: base + 'pages_UI_Display_Images/Client07_借还伞主界面.png', title: '07. 自助服务大厅', desc: '核心主界面，显示个人中心、站点地图、借/还入口。', meta: 'Client07_借还伞主界面.png' },
  { src: base + 'pages_UI_Display_Images/Client08_个人信息页面.png', title: '08. 个人中心', desc: '展示用户信息、余额。', meta: 'Client08_个人信息页面.png' },
  { src: base + 'pages_UI_Display_Images/Client09_服务说明页面.png', title: '09. 服务指南', desc: '内置的帮助文档，说明计费规则与使用方法。', meta: 'Client09_服务说明页面.png' },
  { src: base + 'pages_UI_Display_Images/Client10_站点情况说明页面.png', title: '10. 站点地图详情', desc: '可视化展示各楼栋站点位置、在线情况、剩余雨伞数量。', meta: 'Client10_站点情况说明页面.png' },
  { src: base + 'pages_UI_Display_Images/Client11_借伞页面.png', title: '11. 借伞执行', desc: '系统分配槽位并弹出雨伞。', meta: 'Client11_借伞页面.png' },
  { src: base + 'pages_UI_Display_Images/Client12_还伞页面.png', title: '12. 还伞结算', desc: '归还成功后的结算清单与费用扣除提示。', meta: 'Client12_还伞页面.png' },
]

const adminImages = [
  { src: base + 'pages_UI_Display_Images/Admin01_管理员登录首页面.png', title: '01. 管理员鉴权', desc: '独立的后台管理入口，与用户端物理隔离。', meta: 'Admin01_管理员登录首页面.png' },
  { src: base + 'pages_UI_Display_Images/Admin02_站点雨具概览页面.png', title: '02. 站点全局概览', desc: '监控所有站点的设备在线率。', meta: 'Admin02_站点雨具概览页面.png' },
  { src: base + 'pages_UI_Display_Images/Admin03_站点雨具概览页面.png', title: '03. 站点详情管理', desc: '针对单个站点的库存干预与维护模式。', meta: 'Admin03_站点雨具概览页面.png' },
  { src: base + 'pages_UI_Display_Images/Admin04_用户管理页面.png', title: '04. 用户审计', desc: '全校用户列表，支持密码重置。', meta: 'Admin04_用户管理页面.png' },
  { src: base + 'pages_UI_Display_Images/Admin05_订单流水页面.png', title: '05. 财务流水', desc: '每一笔借还订单的记录查询。', meta: 'Admin05_订单流水页面.png' },
]

const openModal = (src: string) => {
  modalImage.value = src
}

const closeModal = () => {
  modalImage.value = null
}
</script>

<template>
  <div class="app-container">
    <header>
      <div class="container">
        <div class="header-icon">☔</div>
        <h1>Campus RainHub</h1>
        <p class="subtitle">
          "No more being trapped in buildings on rainy days."<br>
          下雨天，再也不用被困在教学楼了。
        </p>
        <a href="https://github.com/Juvin-Chen/Campus-RainHub" target="_blank" class="btn">
          ⭐ View on GitHub
        </a>

        <div class="tech-stack">
          <span class="chip">C++ 17</span>
          <span class="chip">Qt 6.9.3</span>
          <span class="chip">MySQL 8.0</span>
          <span class="chip vue-chip">Vue 3 + TS</span>
        </div>
      </div>
    </header>

    <section class="gallery-section">
      <div class="container">
        <div class="tabs">
          <button 
            :class="['tab-btn', activeTab === 'client' ? 'active' : '']" 
            @click="activeTab = 'client'"
          >
            📱 用户自助终端 (User Client)
          </button>
          <button 
            :class="['tab-btn', activeTab === 'admin' ? 'active' : '']" 
            @click="activeTab = 'admin'"
          >
            🖥️ 综合管理后台 (Admin System)
          </button>
        </div>

        <div v-show="activeTab === 'client'" class="grid">
          <div 
            v-for="(item, index) in clientImages" 
            :key="index" 
            class="card" 
            @click="openModal(item.src)"
          >
            <div class="card-img-wrapper">
              <img :src="item.src" loading="lazy" alt="Preview Image" />
            </div>
            <div class="card-body">
              <div class="card-title">{{ item.title }}</div>
              <div class="card-desc">{{ item.desc }}</div>
              <div class="card-meta">{{ item.meta }}</div>
            </div>
          </div>
        </div>

        <div v-show="activeTab === 'admin'" class="grid">
          <div 
            v-for="(item, index) in adminImages" 
            :key="index" 
            class="card" 
            @click="openModal(item.src)"
          >
            <div class="card-img-wrapper">
              <img :src="item.src" loading="lazy" alt="Preview Image" />
            </div>
            <div class="card-body">
              <div class="card-title">{{ item.title }}</div>
              <div class="card-desc">{{ item.desc }}</div>
              <div class="card-meta">{{ item.meta }}</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Modal -->
    <div 
      class="modal" 
      :class="{ open: modalImage !== null }" 
      @click="closeModal"
    >
      <span class="modal-close" @click.stop="closeModal">&times;</span>
      <img v-if="modalImage" :src="modalImage" @click.stop />
    </div>
  </div>
</template>

<style>
/* 继承并现代化原有的样式 */
:root {
  --primary: #5aa9ff;
  --secondary: #93c5fd;
  --dark-bg: #f5fbff;
  --card-bg: #ffffff;
  --text-main: #0f172a;
  --text-sub: #475569;
  --gradient: linear-gradient(135deg, #5aa9ff 0%, #7dd3fc 60%, #a7f3d0 100%);
  --vue-color: #42b883;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
}

body {
  background-color: var(--dark-bg);
  color: var(--text-main);
  line-height: 1.6;
}

a {
  text-decoration: none;
  color: inherit;
  transition: 0.3s;
}

.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 2rem;
}

/* Header */
header {
  padding: 6rem 0 4rem;
  text-align: center;
  background: radial-gradient(circle at top, #ffffff 0%, #eef6ff 70%);
  border-bottom: 1px solid rgba(15, 23, 42, 0.08);
}

.header-icon {
  font-size: 4rem;
  margin-bottom: 1rem;
}

h1 {
  font-size: 3rem;
  font-weight: 800;
  margin-bottom: 1rem;
  background: var(--gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.subtitle {
  font-size: 1.2rem;
  color: var(--text-sub);
  font-weight: 300;
}

.btn {
  display: inline-block;
  padding: 0.8rem 2.5rem;
  background: var(--primary);
  color: white;
  border-radius: 50px;
  font-weight: 600;
  margin-top: 1.5rem;
  box-shadow: 0 6px 20px rgba(79, 141, 247, 0.25);
  cursor: pointer;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(79, 141, 247, 0.35);
}

.tech-stack {
  margin-top: 2rem;
  display: flex;
  justify-content: center;
  gap: 10px;
  flex-wrap: wrap;
}

.chip {
  background: rgba(2, 132, 199, 0.10);
  padding: 5px 10px;
  border-radius: 4px;
  font-size: 0.8rem;
  color: var(--primary);
  font-weight: 500;
}

.vue-chip {
  color: var(--vue-color);
  background: rgba(66, 184, 131, 0.15);
}

/* Gallery Section */
.gallery-section {
  padding: 4rem 0;
}

.tabs {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
}

.tab-btn {
  background: transparent;
  border: 1px solid var(--text-sub);
  color: var(--text-sub);
  padding: 0.6rem 2rem;
  border-radius: 50px;
  cursor: pointer;
  font-size: 1.1rem;
  transition: all 0.3s ease;
}

.tab-btn.active {
  background: var(--primary);
  border-color: var(--primary);
  color: white;
  box-shadow: 0 0 15px rgba(79, 141, 247, 0.2);
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 2rem;
  animation: fadeIn 0.5s ease;
}

.card {
  background: var(--card-bg);
  border-radius: 16px;
  overflow: hidden;
  border: 1px solid rgba(15, 23, 42, 0.08);
  transition: 0.3s;
  cursor: pointer;
  display: flex;
  flex-direction: column;
}

.card:hover {
  transform: translateY(-5px);
  border-color: var(--secondary);
  box-shadow: 0 14px 40px rgba(15, 23, 42, 0.12);
}

.card-img-wrapper {
  width: 100%;
  height: 240px;
  background: #e2e8f0;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top center;
  transition: 0.5s;
}

.card:hover img {
  transform: scale(1.05);
}

.card-body {
  padding: 1.5rem;
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.card-title {
  font-size: 1.2rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: var(--text-main);
}

.card-desc {
  font-size: 0.95rem;
  color: var(--text-sub);
  line-height: 1.5;
}

.card-meta {
  margin-top: 1rem;
  font-size: 0.8rem;
  color: #64748b;
  font-family: monospace;
}

/* Modal */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.95);
  display: none;
  justify-content: center;
  align-items: center;
  z-index: 9999;
  backdrop-filter: blur(5px);
}

.modal.open {
  display: flex;
  animation: fadeIn 0.2s;
}

.modal img {
  max-width: 95%;
  max-height: 95%;
  border-radius: 4px;
  box-shadow: 0 0 50px rgba(0, 0, 0, 0.5);
  cursor: default;
}

.modal-close {
  position: absolute;
  top: 20px;
  right: 30px;
  color: white;
  font-size: 4rem;
  cursor: pointer;
  line-height: 1;
  transition: color 0.3s;
}

.modal-close:hover {
  color: #ff5c5c;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media(max-width: 768px) {
  h1 {
    font-size: 2rem;
  }
  .grid {
    grid-template-columns: 1fr;
  }
  .card-img-wrapper {
    height: 200px;
  }
}
</style>
