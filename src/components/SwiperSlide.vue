<script setup>
import { ref, onMounted } from 'vue'
const swiper_slide_list = ref([
  'https://my.tcb-life.com.tw/file/3/web_hero_banner.jpg',
  'https://my.tcb-life.com.tw/file/677/web_hero_banner2.png',
  'https://my.tcb-life.com.tw/file/731/史博館 綻放 2880x990.JPG',
  'https://my.tcb-life.com.tw/file/680/電銷-馨健康依靠 0911合庫BN_2880 x 990.jpg',
  'https://my.tcb-life.com.tw/file/681/公關-安心守護計畫20250827_RESIZE-2880X990.JPEG',
])
const raction = ref(false)
const swiper_index = ref(0)
const swiper = ref(null)
let autoPlayTimer = null

const nextSlide = () => {
  raction.value = true

  setTimeout(() => {
    swiper_index.value = (swiper_index.value + 1) % swiper_slide_list.value.length

    raction.value = false
  }, 500)
}

onMounted(() => {
  try {
    autoPlayTimer = setInterval(() => {
      nextSlide()
    }, 3000)
  } catch (err) {
    console.error('onMounted 發生錯誤:', err)
  }
})
</script>
<template>
  <div class="swiper-slide" ref="swiper">
    <img
      :src="
        swiper_slide_list[(swiper_index - 1 + swiper_slide_list.length) % swiper_slide_list.length]
      "
      width="75%"
      draggable="false"
      class="left"
    />
    <img
      :src="swiper_slide_list[swiper_index]"
      width="75%"
      :draggable="false"
      style="transform: scaleY(1.025); position: relative; top: 0.2vw"
    />

    <img
      :src="swiper_slide_list[(swiper_index + 1) % swiper_slide_list.length]"
      width="75%"
      draggable="false"
      class="right"
      :class="{ action: raction }"
    />
  </div>
</template>

<style lang="scss" scoped>
.swiper-slide {
  margin-top: 25px;
  display: block;
  position: relative;
  border-radius: 5vw;
  cursor: pointer;
  box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.5);
  overflow: hidden;
  width: 80%;
  left: 10%;
  img {
    position: relative;
    width: 100%;
    height: 100%;
    &.left {
      position: absolute;
      opacity: 0;
      transform: translate(-100%, 0);
      z-index: 1000;

      &.action {
        transform: translate(0%, 0);
        opacity: 1;
        transition: all 0.5s ease-in-out;
      }
    }

    &.right {
      position: absolute;
      opacity: 0;
      transform: translate(0%, 0%);
      z-index: 1000;

      &.action {
        transform: translate(-100%, 0%);
        opacity: 1;
        transition: all 0.5s ease-in-out;
      }
    }
  }
  @media screen and (max-width: 840px) {
    width: 90%;
    left: 0;
    transform: translateX(5%);
  }
}
</style>
