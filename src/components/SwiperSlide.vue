<script setup>
import { ref } from 'vue' // 不需要 onMounted 了

const swiper_slide_list = ref([
  {
    img: 'https://my.tcb-life.com.tw/file/3/web_hero_banner.jpg',
    url: 'https://my.tcb-life.com.tw/charity-coffee'
  },
  {
    img: 'https://live.staticflickr.com/65535/48636142963_4472ed6c8f.jpg',
    url: 'https://www.youtube.com/?authuser=0'
  },
  {
    img: 'https://my.tcb-life.com.tw/file/677/web_hero_banner2.png',
    url: 'https://my.tcb-life.com.tw/family-care'
  },
  {
    img: 'https://my.tcb-life.com.tw/file/731/史博館 綻放 2880x990.JPG',
    url: 'https://www.tcb-life-online.com.tw/ebiz/member/preregistration?&utm_source=tcblifeBN&utm_medium=BN&utm_campaign=Flower'
  },
  {
    img: 'https://my.tcb-life.com.tw/file/680/電銷-馨健康依靠 0911合庫BN_2880 x 990.jpg',
    url: 'https://mhu.tcb-life.com.tw/landingpage/20180718002/landingpage.aspx?p=eoVIxvGLTDROgjLjpBGUpwGGulod1pzinHG3kyp2Aqs%3d&k=bwWXa3hq4BFeFdDTa1ehVWFOo%2fahlqjqLVRKU3Q3j8WeA1h6yubB%2bKLH26t1o0SgijEadmbtnIiIJCEAnkNCGKgluFyD6qTxaWqZVst5Vox%2fUHp3%2bwDJ54ux7wT2kZj5&si=druanfqdyqgpz24xgxfecbtn'
  },
  {
    img: 'https://my.tcb-life.com.tw/file/681/公關-安心守護計畫20250827_RESIZE-2880X990.JPEG',
    url: 'https://my.tcb-life.com.tw/family-care'
  },
])

const swiper_index = ref(0)
const direction = ref('slide-right') // 核心：控制動畫方向

// 統一的切換邏輯
const changeSlide = (newIndex, customDirection = null) => {
  if (customDirection) {
    direction.value = customDirection
  } else {
    // 自動判斷：如果新索引較小，則從左邊滑入 (slide-left)
    direction.value = newIndex > swiper_index.value ? 'slide-right' : 'slide-left'
  }
  swiper_index.value = newIndex
}

const nextSlide = () => {
  const nextIndex = (swiper_index.value + 1) % swiper_slide_list.value.length
  changeSlide(nextIndex, 'slide-right') // 自動輪播固定向右
}

const prevSlide = () => {
  const prevIndex = (swiper_index.value - 1 + swiper_slide_list.value.length) % swiper_slide_list.value.length
  changeSlide(prevIndex, 'slide-left') // 點擊左箭頭固定向左
}

// 移除 setInterval，因為動畫現在由 CSS 的 @animationend 驅動
</script>

<template>
  <main>
    <section>
      <div class="swiper-slide">
        <!-- 箭頭按鈕 -->
        <button class="arrow-btn left" @click="prevSlide">❮</button>
        <button class="arrow-btn right" @click="nextSlide">❯</button>

        <!-- 圖片切換區 -->
        <Transition :name="direction">
          <div :key="swiper_index" class="slide-item">
            <a :href="swiper_slide_list[swiper_index].url" target="_blank" rel="noopener noreferrer">
              <img :src="swiper_slide_list[swiper_index].img" draggable="false" />
            </a>
          </div>
        </Transition>

        <div class="pagination">
          <span v-for="(item, index) in swiper_slide_list" :key="index" class="dot"
            :class="{ active: swiper_index === index }" @click="changeSlide(index)">
            <div v-if="swiper_index === index" class="inner-bar" @animationend="nextSlide"></div>
          </span>
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

.slide-item {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;

  a {
    display: block;
    width: 100%;
    height: 100%;
    cursor: pointer;
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}

.swiper-slide {
  position: relative;
  width: 85%;
  max-width: 1200px;
  aspect-ratio: 2880 / 990;
  border-radius: 10% 1% 9% 5% / 90% 18% 18% 90%;
  box-shadow: 0px 15px 35px rgba(0, 0, 0, 0.1);
  overflow: hidden;
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

/* 箭頭 */
.arrow-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  color: white;
  font-size: 25px;
  font-weight: bold;
  cursor: pointer;
  z-index: 20;
  padding: 0 5px;
  transition: transform 0.2s ease, opacity 0.3s;
  opacity: 0.7;
  text-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);

  &:hover {
    opacity: 1;
    transform: translateY(-50%) scale(1.2);
  }

  &.left {
    left: 10px;
  }

  &.right {
    right: 10px;
  }
}

/* 點點與進度條樣式 */
.pagination {
  position: absolute;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 12px;
  z-index: 10;

  .dot {
    width: 10px;
    height: 10px;
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 50%;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    transition: all 0.3s cubic-bezier(0.25, 0.8, 0.5, 1);
    border: 1px solid rgba(255, 255, 255, 0.8);
    box-sizing: border-box;

    &.active {
      width: 200px;
      border-radius: 6px;
      background-color: rgba(255, 255, 255, 0.3);
    }

    &:hover:not(.active) {
      background-color: rgb(255, 255, 255);
    }

    .inner-bar {
      position: absolute;
      top: 0;
      left: 0;
      height: 100%;
      background-color: #77db38;
      width: 0;
      animation: dotProgress 5.5s linear forwards;
    }
  }
}

@keyframes dotProgress {
  from {
    width: 0%;
  }

  to {
    width: 100%;
  }
}

/* 動畫邏輯：由右往左滑 (預設) */
.slide-right-enter-from {
  transform: translateX(100%);
}

.slide-right-leave-to {
  transform: translateX(-100%);
}

/* 動畫邏輯：由左往右滑 (後退) */
.slide-left-enter-from {
  transform: translateX(-100%);
}

.slide-left-leave-to {
  transform: translateX(100%);
}

/* 動畫過程設定 */
.slide-right-enter-active,
.slide-right-leave-active,
.slide-left-enter-active,
.slide-left-leave-active {
  transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}
</style>