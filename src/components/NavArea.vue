<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isNavSticky = ref(false)
const stickyRef = ref(null)
const menuSelector = ref(0)

let leaveTimer = null
let observer = null

const handleMouseEnter = (index) => {
  if (index === 6) return
  if (leaveTimer) clearTimeout(leaveTimer)
  menuSelector.value = index
}

const handleMouseLeave = () => {
  leaveTimer = setTimeout(() => {
    menuSelector.value = 0
  }, 150)
}

const toggleSearch = () => {
  menuSelector.value = menuSelector.value === 6 ? 0 : 6
}

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => {
      isNavSticky.value = !entry.isIntersecting
    },
    { threshold: 0 },
  )
  if (stickyRef.value) observer.observe(stickyRef.value)
})

onUnmounted(() => {
  if (observer) observer.disconnect()
  if (leaveTimer) clearTimeout(leaveTimer)
})
</script>

<template>
  <div ref="stickyRef" class="sticky-trigger"></div>
  <nav :class="{ 'is-sticky': isNavSticky }">
    <div class="nav-logo">
      <img
        src="https://my.tcb-life.com.tw/assets/%E5%90%88%E5%BA%AB%E4%BA%BA%E5%A3%BDLOGO-hrqQj5ac.svg"
        alt="LOGO"
      />
    </div>

    <div class="nav-links">
      <div class="nav-item" @mouseenter="handleMouseEnter(1)" @mouseleave="handleMouseLeave">
        <button class="nav-btn">保戶服務</button>
        <Transition name="fade">
          <div class="dropdown-menu" v-if="menuSelector === 1"></div>
        </Transition>
      </div>

      <div class="nav-item">
        <button class="nav-btn">安心守護</button>
      </div>

      <div class="nav-item" @mouseenter="handleMouseEnter(2)" @mouseleave="handleMouseLeave">
        <button class="nav-btn">所有商品</button>
        <Transition name="fade">
          <div class="dropdown-menu" v-if="menuSelector === 2"></div>
        </Transition>
      </div>

      <div class="nav-item" @mouseenter="handleMouseEnter(3)" @mouseleave="handleMouseLeave">
        <button class="nav-btn">公平待客</button>
        <Transition name="fade">
          <div class="dropdown-menu" v-if="menuSelector === 3"></div>
        </Transition>
      </div>

      <div class="nav-item" @mouseenter="handleMouseEnter(4)" @mouseleave="handleMouseLeave">
        <button class="nav-btn">保險知識庫</button>
        <Transition name="fade">
          <div class="dropdown-menu" v-if="menuSelector === 4"></div>
        </Transition>
      </div>

      <div class="nav-item" @mouseenter="handleMouseEnter(5)" @mouseleave="handleMouseLeave">
        <button class="nav-btn">關於我們</button>
        <Transition name="fade">
          <div class="dropdown-menu" v-if="menuSelector === 5"></div>
        </Transition>
      </div>

      <div class="nav-item search-item">
        <button class="nav-btn search-btn" @click="toggleSearch">🔍</button>
        <Transition name="fade">
          <div class="dropdown-menu search-menu" v-if="menuSelector === 6"></div>
        </Transition>
      </div>
    </div>
  </nav>
  <br />
</template>

<style lang="scss" scoped>
.sticky-trigger {
  height: 1px;
  width: 100%;
}

nav {
  position: sticky;
  top: 15px;
  z-index: 100;
  width: 90%;
  max-width: 1440px;
  height: 60px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  padding: 0 30px;
  background-color: #ffffff00;
  border-radius: 100px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);

  &.is-sticky {
    width: 95%;
    background-color: rgba(255, 255, 255, 1);
    backdrop-filter: blur(10px);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  }

  .nav-logo {
    margin-right: 20px;
    img {
      height: 35px;
    }
  }

  .nav-links {
    flex: 1;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .nav-item {
    position: relative;
    display: flex;
    justify-content: center;
    flex: 1;
  }

  .nav-btn {
    all: unset;
    font-size: 16px;
    color: #333;
    padding: 8px 16px;
    border-radius: 50px;
    cursor: pointer;
    white-space: nowrap;
    transition: all 0.2s;

    &:hover,
    &.active {
      background-color: #05bf90;
      color: #fff;
    }
  }

  .dropdown-menu {
    position: absolute;
    top: 50px;
    left: 50%;
    transform: translateX(-50%);
    width: 60vw;
    height: 300px;
    background: #fff;
    border-radius: 20px;
    box-shadow: 0 20px 50px rgba(0, 0, 0, 0.15);
    z-index: 110;
  }

  .search-menu {
    left: auto;
    right: 0;
    transform: translateX(0);
    width: 350px;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition:
    opacity 0.25s,
    transform 0.25s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translate(-50%, 15px);
}

.search-item .fade-enter-from,
.search-item .fade-leave-to {
  transform: translateY(15px);
}

@media (max-width: 840px) {
  nav {
    .nav-btn {
      font-size: 14px;
      padding: 6px 10px;
    }
    .nav-logo img {
      height: 28px;
    }
  }
}
</style>
