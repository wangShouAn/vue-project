<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'

const isNavSticky = ref(false)
const stickyTrigger = ref(null)
const menuSelector = ref(0)
const searchInput = ref(null)

let leaveTimer = null
let observer = null

// 導航資料設定
const navList = [
  { id: 1, title: '保戶服務', hasDropdown: true },
  { id: 2, title: '安心守護', hasDropdown: false },
  { id: 3, title: '所有商品', hasDropdown: true },
  { id: 4, title: '公平待客', hasDropdown: true },
  { id: 5, title: '保險知識庫', hasDropdown: true },
  { id: 6, title: '關於我們', hasDropdown: true },
]

const handleMouseEnter = (id) => {
  if (leaveTimer) clearTimeout(leaveTimer)
  menuSelector.value = id
}

const handleMouseLeave = () => {
  leaveTimer = setTimeout(() => {
    menuSelector.value = 0
  }, 200) // 略微增加緩衝時間
}

const toggleSearch = async () => {
  menuSelector.value = menuSelector.value === 99 ? 0 : 99
  if (menuSelector.value === 99) {
    await nextTick()
    searchInput.value?.focus() // 開啟搜尋時自動聚焦
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
  if (leaveTimer) clearTimeout(leaveTimer)
})
</script>
<template>
  <div ref="stickyTrigger" class="sticky-trigger"></div>

  <nav :class="{ 'is-sticky': isNavSticky }">
    <div class="nav-container">
      <div class="nav-logo">
        <img
          src="https://my.tcb-life.com.tw/assets/%E5%90%88%E5%BA%AB%E4%BA%BA%E5%A3%BDLOGO-hrqQj5ac.svg"
          alt="LOGO"
        />
      </div>

      <div class="nav-links">
        <div
          v-for="item in navList"
          :key="item.id"
          class="nav-item"
          @mouseenter="item.hasDropdown && handleMouseEnter(item.id)"
          @mouseleave="handleMouseLeave"
        >
          <button class="nav-btn" :class="{ active: menuSelector === item.id }">
            {{ item.title }}
          </button>

          <Transition name="fade-slide">
            <div class="dropdown-menu" v-if="menuSelector === item.id">
              <div class="transparent-bridge"></div>
              <div class="menu-content">
                <div v-if="item.id === 1" class="promo-box">
                  <img
                    src="https://my.tcb-life.com.tw/api/assets/2a009399-4329-4913-98f4-e7e896c4c17f"
                  />
                </div>
                <p>這裡顯示 {{ item.title }} 的細節內容</p>
              </div>
            </div>
          </Transition>
        </div>

        <div class="nav-item search-item">
          <button class="nav-btn search-btn" @click="toggleSearch">🔍</button>
          <Transition name="fade-slide">
            <div class="dropdown-menu search-menu" v-if="menuSelector === 99">
              <div class="transparent-bridge"></div>
              <input
                ref="searchInput"
                type="text"
                placeholder="請輸入關鍵字..."
                class="search-input"
              />
            </div>
          </Transition>
        </div>
      </div>
    </div>
  </nav>
</template>
<style lang="scss" scoped>
.sticky-trigger {
  height: 1px;
  position: absolute;
  top: 0;
}

nav {
  position: sticky;
  top: 15px;
  z-index: 1000;
  width: 90vw;
  max-width: 1200px;
  height: 70px;
  margin: 0 auto;
  background-color: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(5px);
  border-radius: 50px;
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  display: flex;
  align-items: center;

  &.is-sticky {
    width: 85%;
    background-color: #fff;
    box-shadow: 0 10px 40px rgba(0, 0, 0, 0.08);
    top: 10px;
  }

  .nav-container {
    width: 100%;
    display: flex;
    align-items: center;
    padding: 0 25px;
  }

  .nav-logo img {
    height: 32px;
    margin-right: 15px;
  }

  .nav-links {
    flex: 1;
    display: flex;
    justify-content: space-around;
  }

  .nav-item {
    position: relative;

    .nav-btn {
      all: unset;
      font-size: clamp(14px, 1.1vw, 16px);
      font-weight: 500;
      color: #444;
      padding: 10px 18px;
      border-radius: 25px;
      cursor: pointer;
      transition: 0.3s;

      &:hover,
      &.active {
        background-color: #05bf90;
        color: #fff;
      }
    }
  }

  /* 下拉選單核心優化 */
  .dropdown-menu {
    position: absolute;
    top: 55px; // 與按鈕保持適當距離
    left: 50%;
    transform: translateX(-50%);
    width: 500px;
    background: #fff;
    border-radius: 16px;
    box-shadow: 0 15px 45px rgba(0, 0, 0, 0.12);
    padding: 20px;

    .transparent-bridge {
      position: absolute;
      top: -20px; // 填補按鈕與選單間的空隙
      left: 0;
      right: 0;
      height: 20px;
    }
  }

  .search-menu {
    width: 300px;
    right: 0;
    left: auto;
    transform: none;

    .search-input {
      width: 100%;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 8px;
    }
  }
}

/* 動畫效果 */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition:
    opacity 0.3s,
    transform 0.3s;
}

.fade-slide-enter-from {
  opacity: 0;
  transform: translate(-50%, 20px);
}
.fade-slide-leave-to {
  opacity: 0;
  transform: translate(-50%, 10px);
}

// 針對搜尋框的動畫微調
.search-item .fade-slide-enter-from,
.search-item .fade-slide-leave-to {
  transform: translateY(10px);
}
</style>
