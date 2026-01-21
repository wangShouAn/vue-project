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
  if (raction.value) return; // 防止動畫中重複點擊

  raction.value = true;

  // 動和畫時間 (500ms) 結束後，再切換資料
  setTimeout(() => {
    swiper_index.value = (swiper_index.value + 1) % swiper_slide_list.value.length;
    raction.value = false;
    // 注意：這裡 raction 變回 false 的瞬間，圖片索引已換成下一張，
    // 且該圖預設就是 translateX(0)，所以視覺上會無縫接軌。
  }, 500);
};

onMounted(() => {
  autoPlayTimer = setInterval(nextSlide, 3500)
})
</script>

<template>
  <main>
    <section>
      <div class="swiper-slide">
        <img :src="swiper_slide_list[swiper_index]" draggable="false" />
      </div>
    </section>

  </main>
</template>

<style lang="scss" scoped>
swiper-slide {
  margin-top: 25px;
  display: block;
  position: relative;
  width: 75%; // 設定寬度
  margin-left: auto;
  margin-right: auto;
  aspect-ratio: 2880 / 990; // 根據你圖片的原始比例設定高度
  border-radius: 5vw;
  box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.5);
  overflow: hidden;
  background-color: #f0f0f0; // 預載入背景色

  .swiper-slide {
    margin-top: 25px;
    display: block;
    position: relative;

    /* --- 置中關鍵設定 --- */
    width: 85%; // 調整 Banner 寬度
    margin-left: auto; // 自動推擠左側空間
    margin-right: auto; // 自動推擠右側空間
    /* ------------------ */

    aspect-ratio: 2880 / 990;

    /* ✨ 左右弧度不一樣的精緻寫法 ✨ */
    border-radius: 40% 60% 40% 70% / 60% 50% 70% 40%;

    box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.15);
    overflow: hidden;
    background-color: #f0f0f0;

    img {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      object-fit: cover; // 確保圖片不變形地填滿置中容器
    }
  }}</style>
