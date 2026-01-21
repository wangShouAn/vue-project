<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
const isNavSticky = ref(false)
const Sticky = ref(null)
const menuSeletor = ref(0)

const laction = ref(false)

let leaveTimer = null

let observer = null

onMounted(() => {
  try {
    observer = new IntersectionObserver(
      ([entry]) => {
        isNavSticky.value = !entry.isIntersecting
      },
      { threshold: 0 },
    )

    if (Sticky.value) {
      observer.observe(Sticky.value)
    } else {
      console.warn('Sticky element not found')
    }
  } catch (err) {
    console.error('onMounted 發生錯誤:', err)
  }
})

onUnmounted(() => {
  if (observer) observer.disconnect()
  if (leaveTimer) clearTimeout(leaveTimer)
  if (autoPlayTimer) clearInterval(autoPlayTimer)
})

const handleMouseEnter = (index) => {
  if (leaveTimer) clearTimeout(leaveTimer)
  menuSeletor.value = index
}

const handleMouseLeave = () => {
  leaveTimer = setTimeout(() => {
    menuSeletor.value = 0
  }, 150)
}
</script>
<template>
  <div ref="Sticky" class="Sticky"></div>
  <nav :class="{ 'is-sticky': isNavSticky }">
    <img
      src="https://my.tcb-life.com.tw/assets/%E5%90%88%E5%BA%AB%E4%BA%BA%E5%A3%BDLOGO-hrqQj5ac.svg"
    />

    <item>
      <button @mouseenter="handleMouseEnter(1)" @mouseleave="handleMouseLeave">保戶服務</button>
      <menu
        @mouseenter="handleMouseEnter(1)"
        @mouseleave="handleMouseLeave"
        v-if="menuSeletor === 1"
      ></menu>
    </item>

    <button>安心守護</button>

    <item>
      <button @mouseenter="handleMouseEnter(2)" @mouseleave="handleMouseLeave">所有商品</button>
      <menu
        @mouseenter="handleMouseEnter(2)"
        @mouseleave="handleMouseLeave"
        v-if="menuSeletor === 2"
      ></menu>
    </item>

    <item>
      <button @mouseenter="handleMouseEnter(3)" @mouseleave="handleMouseLeave">公平待客</button>
      <menu
        @mouseenter="handleMouseEnter(3)"
        @mouseleave="handleMouseLeave"
        v-if="menuSeletor === 3"
      ></menu>
    </item>

    <item>
      <button @mouseenter="handleMouseEnter(4)" @mouseleave="handleMouseLeave">保險知識庫</button>
      <menu
        @mouseenter="handleMouseEnter(4)"
        @mouseleave="handleMouseLeave"
        v-if="menuSeletor === 4"
      ></menu>
    </item>

    <item>
      <button @mouseenter="handleMouseEnter(5)" @mouseleave="handleMouseLeave">關於我們</button>
      <menu
        @mouseenter="handleMouseEnter(5)"
        @mouseleave="handleMouseLeave"
        v-if="menuSeletor === 5"
      ></menu>
    </item>

    <search @mouseenter="handleMouseEnter(6)" @mouseleave="handleMouseLeave">🔍</search>
    <menu
      @mouseenter="handleMouseEnter(6)"
      @mouseleave="handleMouseLeave"
      v-if="menuSeletor === 6"
    ></menu>
  </nav>
</template>

<style lang="scss" scoped>
nav {
  font-size: 1vw;
  transition:
    background-color 0.3s ease-in-out,
    box-shadow 0.3s ease-in-out;
  position: sticky;
  top: 0px;
  z-index: 100;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 2.5vw;
  padding: 0.5vw 1vw;
  width: 80%;
  scale: 0.9;
  margin: 0 auto;
  border-radius: 100px;
  background-color: #ffffff00;

  &.is-sticky {
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    background-color: #fff;
  }

  img {
    height: 2vw;
  }

  button {
    all: unset;
    padding: 0.5vw 1vw;
    margin: 0;
    border-radius: 1vw;
    cursor: pointer;

    &:hover {
      background-color: #05bf90;
      color: #fff;
    }
  }

  search {
    cursor: pointer;
  }

  menu {
    position: absolute;
    height: 200px;
    width: 200px;
    background-color: #fff;
    top: 75%;
    transform: translate(-35%, 0%);
    border-radius: 10px;
  }
}
</style>
