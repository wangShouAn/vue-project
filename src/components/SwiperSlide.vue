<script setup>
import { ref, onMounted } from 'vue'

const swiper_slide_list = ref([
  'https://my.tcb-life.com.tw/file/3/web_hero_banner.jpg',
  'https://live.staticflickr.com/65535/48636142963_4472ed6c8f.jpg',
  'https://my.tcb-life.com.tw/file/677/web_hero_banner2.png',
  'https://my.tcb-life.com.tw/file/731/史博館 綻放 2880x990.JPG',
  'https://my.tcb-life.com.tw/file/680/電銷-馨健康依靠 0911合庫BN_2880 x 990.jpg',
  'https://my.tcb-life.com.tw/file/681/公關-安心守護計畫20250827_RESIZE-2880X990.JPEG',
])

const swiper_index = ref(0)
let autoPlayTimer = null

const direction = ref('slide-right') // 預設方向

const changeSlide = (newIndex) => {
  // 比較新舊索引決定方向
  if (newIndex > swiper_index.value) {
    direction.value = 'slide-right' // 從右邊進來
  } else {
    direction.value = 'slide-left'  // 從左邊進來
  }

  swiper_index.value = newIndex
}

const nextSlide = () => {
  const nextIndex = (swiper_index.value + 1) % swiper_slide_list.value.length
  changeSlide(nextIndex)
}

onMounted(() => {
  autoPlayTimer = setInterval(nextSlide, 3500)
})
</script>

<template>
  <main>
    <section>
      <div class="swiper-slide">
        <Transition :name="direction">
          <img :key="swiper_index" :src="swiper_slide_list[swiper_index]" draggable="false" />
        </Transition>

        <div class="pagination">
          <span v-for="(item, index) in swiper_slide_list" :key="index" class="dot"
            :class="{ active: swiper_index === index }" @click="changeSlide(index)"></span>
        </div>
      </div>
    </section>
  </main>
</template>

<style lang="scss" scoped>
section {
  width: 100%;
  display: flex;
  justify-content: center;
  padding: 20px 0;
}

.swiper-slide {
  position: relative;
  width: 85%;
  max-width: 1200px;
  aspect-ratio: 2880 / 990;

  /* 你的特殊弧度 */
  border-radius: 10% 96% 9% 5% / 90% 5% 8% 90%;
  box-shadow: 0px 15px 35px rgba(0, 0, 0, 0.1);
  overflow: hidden; // 裁切滑動中的圖片
  background-color: #f0f0f0;

  img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}

.pagination {
  position: absolute;
  bottom: 20px;
  /* 距離底部距離 */
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 10px;
  /* 點點之間的間距 */
  z-index: 10;
  /* 確保在圖片上方 */

  .dot {
    width: 12px;
    height: 12px;
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 50%;
    cursor: pointer;
    transition: all 0.3s ease;
    
    &.active {
      width: 30px;
      /* 變長像進度條 */
      border-radius: 6px;
      background-color: #82e159;
    }

    &:hover {
      background-color: #82e159;
    }
  }
}

/* --- 從右滑向左 --- */
.slide-right-enter-from { transform: translateX(100%); }
.slide-right-leave-to { transform: translateX(-100%); }

/* --- 從左滑向右 --- */
.slide-left-enter-from { transform: translateX(-100%); }
.slide-left-leave-to { transform: translateX(100%); }

/* 共同設定：進場與離開的過渡效果 */
.slide-right-enter-active, .slide-right-leave-active,
.slide-left-enter-active, .slide-left-leave-active {
  transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}
</style>
