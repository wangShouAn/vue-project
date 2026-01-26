<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isVisible = ref(false)

function topFunction() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function handleScroll() {
  isVisible.value = window.scrollY > 200
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <Transition>
    <button v-show="isVisible" @click="topFunction()">^</button>
  </Transition>
</template>

<style scoped lang="scss">
button {
  z-index: 59999;
  border: none;
  position: fixed;
  padding: 0.5vw;
  width: 3.5vw;
  right: 5vw;
  bottom: 5vw;
  background-color: #008e6bb9;
  color: #fff;
  border-radius: 100%;

  font-size: 2vw;
  text-align: center;
  &:hover {
    background-color: #008e6b;
    cursor: pointer;
  }
  @media screen and (max-width: 840px) {
    font-size: 4vw;
    padding: 1vw;
    width: 7vw;
  }
}
.v-enter-active,
.v-leave-active {
  transition: all 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  transform: translateY(10vw);
  opacity: 0;
}
</style>
