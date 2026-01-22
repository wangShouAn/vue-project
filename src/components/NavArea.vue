<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'

// 狀態控制
const isNavSticky = ref(false)
const stickyTrigger = ref(null)
const menuSelector = ref(0)
const searchInput = ref(null)

let leaveTimer = null
let observer = null

// 導覽列資料定義
const navItems = [
  { id: 1, title: '保戶服務', hasMega: true },
  { id: 2, title: '安心守護', hasMega: false },
  { id: 3, title: '所有商品', hasMega: true },
  { id: 4, title: '公平待客', hasMega: true },
  { id: 5, title: '保險知識庫', hasMega: true },
  { id: 6, title: '關於我們', hasMega: true },
]

// 模擬保戶服務內容 (對應你提供的圖片)
const serviceContent = {
  img: 'https://my.tcb-life.com.tw/api/assets/2a009399-4329-4913-98f4-e7e896c4c17f',
  columns: [
    {
      links: [
        { name: '理賠專區' },
        { name: '匯率查詢' },
        { name: '電子單據服務' },
        { name: '行動身分識別身分認證服務' },
        { name: '外來人口「新式統一證號」' },
      ],
    },
    {
      links: [
        { name: '表單下載' },
        { name: '保戶專區' },
        { name: '常見問題' },
        { name: '聯絡我們' },
        { name: '尊榮VIP' },
      ],
    },
    {
      groups: [
        { title: '契約變更作業', links: [{ name: '契約變更' }, { name: '保全進度查詢' }] },
        { title: '保單借款執行專區', links: [] },
      ],
    },
  ],
}

// 事件處理
const handleOpen = (id) => {
  if (leaveTimer) clearTimeout(leaveTimer)
  menuSelector.value = id
}

const handleClose = () => {
  leaveTimer = setTimeout(() => {
    menuSelector.value = 0
  }, 200)
}

const toggleSearch = async () => {
  menuSelector.value = menuSelector.value === 99 ? 0 : 99
  if (menuSelector.value === 99) {
    await nextTick()
    searchInput.value?.focus()
  }
}

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => {
      isNavSticky.value = !entry.isIntersecting
    },
    { threshold: 0 },
  )
  if (stickyTrigger.value) observer.observe(stickyTrigger.value)
})

onUnmounted(() => {
  if (observer) observer.disconnect()
})
</script>

<template>
  <div ref="stickyTrigger" class="sticky-anchor"></div>

  <nav :class="{ 'is-sticky': isNavSticky }">
    <div class="nav-wrap">
      <div class="logo">
        <img
          src="https://my.tcb-life.com.tw/assets/%E5%90%88%E5%BA%AB%E4%BA%BA%E5%A3%BDLOGO-hrqQj5ac.svg"
          alt="TCB Life"
        />
      </div>

      <div class="menu-list">
        <div
          v-for="item in navItems"
          :key="item.id"
          class="menu-item"
          @mouseenter="handleOpen(item.id)"
          @mouseleave="handleClose"
        >
          <button class="menu-btn" :class="{ active: menuSelector === item.id }">
            {{ item.title }}
          </button>

          <Transition name="mega-fade">
            <div class="mega-dropdown" v-if="menuSelector === item.id && item.hasMega">
              <div class="bridge"></div>
              <div class="mega-inner">
                <div class="mega-banner">
                  <img :src="serviceContent.img" alt="banner" />
                </div>
                <div class="mega-grid">
                  <div v-for="(col, i) in serviceContent.columns" :key="i" class="mega-col">
                    <ul v-if="col.links" class="link-group">
                      <li v-for="link in col.links" :key="link.name">
                        <a href="#">{{ link.name }} <i class="arrow">›</i></a>
                      </li>
                    </ul>
                    <div v-if="col.groups">
                      <div v-for="group in col.groups" :key="group.title" class="sub-section">
                        <h4 class="sub-title">
                          {{ group.title }} <i v-if="!group.links.length" class="arrow">›</i>
                        </h4>
                        <ul class="link-group">
                          <li v-for="sub in group.links" :key="sub.name">
                            <a href="#">{{ sub.name }} <i class="arrow">›</i></a>
                          </li>
                        </ul>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </Transition>
        </div>

        <div class="menu-item">
          <button class="menu-btn" @click="toggleSearch">🔍</button>
          <Transition name="mega-fade">
            <div class="search-bar" v-if="menuSelector === 99">
              <input ref="searchInput" type="text" placeholder="搜尋關鍵字..." />
            </div>
          </Transition>
        </div>
      </div>
    </div>
  </nav>
</template>

<style lang="scss" scoped>
// 變數定義
$primary: #05bf90;
$bg-gray: #f4f6f8;

.sticky-anchor {
  height: 1px;
  position: absolute;
  top: 0;
}

nav {
  position: sticky;
  top: 15px;
  z-index: 999;
  width: 92%;
  max-width: 1400px;
  height: 80px;
  margin: 0 auto;
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(8px);
  border-radius: 100px;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  display: flex;
  align-items: center;

  &.is-sticky {
    width: 80%;
    top: 10px;
    background: #fff;
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.1);
  }

  .nav-wrap {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 40px;
  }

  .logo img {
    height: 38px;
  }

  .menu-list {
    display: flex;
    gap: 8px;
  }

  .menu-btn {
    all: unset;
    padding: 12px 20px;
    font-size: 16px;
    font-weight: 500;
    color: #333;
    border-radius: 30px;
    cursor: pointer;
    transition: 0.3s;

    &:hover,
    &.active {
      background: $primary;
      color: #fff;
    }
  }
}

// Mega Menu 核心樣式
.mega-dropdown {
  position: absolute;
  top: 70px;
  left: 50%;
  transform: translateX(-50%);
  width: 900px;
  background: $bg-gray;
  border-radius: 20px;
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.15);
  padding: 35px;

  .bridge {
    position: absolute;
    top: -20px;
    left: 0;
    width: 100%;
    height: 25px;
  }

  .mega-inner {
    display: flex;
    gap: 40px;
  }

  .mega-banner {
    flex: 0 0 280px;
    img {
      width: 100%;
      border-radius: 15px;
    }
  }

  .mega-grid {
    flex: 1;
    display: grid;
    grid-template-columns: 1.2fr 1fr 1.2fr;
    gap: 25px;
  }

  .link-group {
    list-style: none;
    padding: 0;
    margin: 0;
    li {
      margin-bottom: 15px;
      a {
        text-decoration: none;
        color: #555;
        font-size: 15px;
        display: flex;
        align-items: center;
        &:hover {
          color: $primary;
          .arrow {
            transform: translateX(3px);
          }
        }
      }
    }
  }

  .sub-section {
    margin-bottom: 25px;
  }
  .sub-title {
    font-size: 16px;
    color: #333;
    margin-bottom: 12px;
    display: flex;
    align-items: center;
  }

  .arrow {
    margin-left: auto;
    color: $primary;
    font-style: normal;
    font-weight: bold;
    font-size: 18px;
    transition: 0.2s;
  }
}

// 搜尋條
.search-bar {
  position: absolute;
  top: 70px;
  right: 0;
  width: 320px;
  background: #fff;
  padding: 15px;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  input {
    width: 100%;
    padding: 12px;
    border: 1px solid #eee;
    border-radius: 8px;
    outline: none;
    &:focus {
      border-color: $primary;
    }
  }
}

// 動畫效果
.mega-fade-enter-active,
.mega-fade-leave-active {
  transition:
    opacity 0.3s,
    transform 0.3s;
}
.mega-fade-enter-from {
  opacity: 0;
  transform: translate(-50%, 20px);
}
.mega-fade-leave-to {
  opacity: 0;
  transform: translate(-50%, 10px);
}
</style>
