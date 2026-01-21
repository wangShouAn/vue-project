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

const nextSlide = () => {
  // 只需要改變 index，剩下的交給 Transition 組件處理
  swiper_index.value = (swiper_index.value + 1) % swiper_slide_list.value.length;
};

onMounted(() => {
  autoPlayTimer = setInterval(nextSlide, 3500)
})
</script>

<template>
  <main>
    <section>
      <div class="swiper-slide">
        <Transition name="slide-right">
          <img 
            :key="swiper_index"
            :src="swiper_slide_list[swiper_index]" 
            draggable="false" 
          />
        </Transition>
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

/* ✨ 向右滑動動畫邏輯 ✨ */

// 1. 新圖片從右邊外側進場 (-100% 代表左，100% 代表右)
.slide-right-enter-from {
  transform: translateX(100%); 
}

// 2. 舊圖片向右邊消失
.slide-right-leave-to {
  transform: translateX(-100%);
}

// 3. 設定動畫過程
.slide-right-enter-active,
.slide-right-leave-active {
  transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}
</style>
