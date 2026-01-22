<template>
  <div class="video-section-container">
    <!-- 影片播放區塊 -->
    <video-area-block @touchstart="handleTouchStart" @touchend="handleTouchEnd">
      <div class="video-frame-wrapper">
        <!-- 影片過渡動畫 -->
        <transition :name="slideDirection">
          <div :key="activeIndex" class="video-slide">
            <!-- 底層預覽圖：防止 iframe 加載過程出現黑屏 -->
            <img
              :src="`https://img.youtube.com/vi/${videoList[activeIndex].id}/hqdefault.jpg`"
              class="video-placeholder"
            />

            <!-- 上層影片：加載完成後才透過 opacity 顯示 -->
            <iframe
              id="main-video"
              :src="currentVideoUrl"
              title="主影片"
              frameborder="0"
              allow="
                accelerometer;
                autoplay;
                clipboard-write;
                encrypted-media;
                gyroscope;
                picture-in-picture;
                web-share;
              "
              allowfullscreen
              :class="{ 'is-loaded': iframeLoaded }"
              @load="handleIframeLoad"
            ></iframe>
          </div>
        </transition>
      </div>

      <video-content>
        <h1>影音專區</h1>
        <video-card>
          <div class="text-animation-container">
            <transition name="fade-smooth" mode="out-in">
              <div :key="activeIndex">
                <h2 id="video-title">{{ currentTitle }}</h2>
                <p id="video-desc">{{ currentDesc }}</p>
              </div>
            </transition>
          </div>
        </video-card>
      </video-content>
    </video-area-block>

    <!-- 底部操作區 -->
    <video-action>
      <video-pagination>
        <button
          v-for="(video, index) in videoList"
          :key="video.id"
          :class="{ active: activeIndex === index }"
          @click="handleButtonClick(index)"
        >
          <img :src="`https://img.youtube.com/vi/${video.id}/hqdefault.jpg`" />
        </button>
      </video-pagination>

      <video-action-more-btn-container>
        <button class="lookMore">看更多<span class="arrow-icon">→</span></button>
      </video-action-more-btn-container>
    </video-action>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const videoList = [
  {
    id: 'fYnGJwbBBIQ',
    title: '合庫人壽校園巡講精華合輯',
    desc: '風險管理不是害怕未來，而是讓選擇更多、夢想走得更遠。 邀請你一起回顧這段溫慢的校園旅程。',
  },
  {
    id: 'bn0xi52L1QU',
    title: '如何規劃人生第一張保單？',
    desc: '專家告訴你，年輕人投保的三大重點，讓你的未來更有保障，不用擔心意外。',
  },
  {
    id: 'kH3Wyr3lw-Q',
    title: '投資型保單怎麼選？',
    desc: '深入淺出解析投資型保單的運作原理，讓你理財更安心，資產配置更靈活。',
  },
  {
    id: 'lv6W6-24SRw',
    title: '退休生活提早佈局',
    desc: '不要等到老了才開始，現在就為你的樂活退休做準備，打造無憂的老後生活。',
  },
]

const activeIndex = ref(0)
const isAnimating = ref(false)
const iframeLoaded = ref(false) // 追蹤目前 iframe 是否載入完成
const slideDirection = ref('slide-left')

const currentVideoUrl = computed(
  () => `https://www.youtube.com/embed/${videoList[activeIndex.value].id}?autoplay=0&rel=0`,
)
const currentTitle = computed(() => videoList[activeIndex.value].title)
const currentDesc = computed(() => videoList[activeIndex.value].desc)

let touchStartX = 0
let touchEndX = 0

const handleTouchStart = (e) => {
  touchStartX = e.changedTouches[0].screenX
}

const handleTouchEnd = (e) => {
  touchEndX = e.changedTouches[0].screenX
  handleSwipe()
}

const handleSwipe = () => {
  const swipeThreshold = 50
  if (touchStartX - touchEndX > swipeThreshold) {
    const nextIndex = (activeIndex.value + 1) % videoList.length
    handleButtonClick(nextIndex)
  } else if (touchEndX - touchStartX > swipeThreshold) {
    const prevIndex = (activeIndex.value - 1 + videoList.length) % videoList.length
    handleButtonClick(prevIndex)
  }
}

const handleButtonClick = (index) => {
  if (index === activeIndex.value || isAnimating.value) return

  slideDirection.value = index > activeIndex.value ? 'slide-left' : 'slide-right'

  isAnimating.value = true
  iframeLoaded.value = false // 切換時重置載入狀態，顯示預覽圖
  activeIndex.value = index

  // 定時鎖定解除
  setTimeout(() => {
    isAnimating.value = false
  }, 500)
}

const handleIframeLoad = () => {
  // 當 iframe 內部 HTML 載入後觸發，讓影片平滑顯現
  iframeLoaded.value = true
}
</script>

<style lang="scss" scoped>
.video-section-container {
  background-color: #fafafa;
  width: 100%;
  user-select: none;
  overflow: hidden;
}

video-area-block {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 4vw auto;
  margin-bottom: 0.5vw;
  padding: 0 16vw;

  .video-frame-wrapper {
    width: 31vw;
    height: 17vw;
    border-radius: 1vw;
    background-color: #000;
    position: relative;
    overflow: hidden;
    transform: translateZ(0);
    contain: strict;

    .video-slide {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      will-change: transform;
    }

    .video-placeholder {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
      z-index: 1;
    }

    iframe {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border: none;
      z-index: 2;
      opacity: 0; /* 預設隱藏 */
      transition: opacity 0.4s ease-in; /* 平滑顯示影片 */

      &.is-loaded {
        opacity: 1; /* 載入完成後顯示 */
      }
    }
  }

  video-content {
    height: 17vw;
    width: 24vw;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    background-color: #fff;
    padding-left: 2vw;

    h1 {
      font-size: 1.5vw;
      margin: 0;
      padding: 0;
      color: #008765;
      width: 100%;
    }

    video-card {
      display: flex;
      flex-direction: column;
      border-radius: 1vw;
      background-color: #f6f4ed;
      height: 100%;
      width: 100%;
      justify-content: center;
      align-items: flex-start;
      padding: 2vw;
      box-sizing: border-box;
      overflow: hidden;
    }
  }
}

.text-animation-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;

  h2 {
    font-size: 1vw;
    margin: 0;
    margin-bottom: 1vw;
    padding: 0;
    text-align: left;
    line-height: 1.4;
    color: #333;
  }

  p {
    font-size: 0.8vw;
    margin: 0;
    padding: 0;
    line-height: 1.6;
    color: #555;
  }
}

// --- 動畫樣式 ---

.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition:
    transform 0.45s cubic-bezier(0.25, 1, 0.5, 1),
    opacity 0.4s ease;
}

.slide-left-enter-active,
.slide-right-enter-active {
  z-index: 2;
}

.slide-left-enter-from {
  transform: translateX(100%);
  opacity: 0;
}
.slide-left-leave-to {
  transform: translateX(-30%);
  opacity: 0;
}

.slide-right-enter-from {
  transform: translateX(-100%);
  opacity: 0;
}
.slide-right-leave-to {
  transform: translateX(30%);
  opacity: 0;
}

.fade-smooth-enter-active,
.fade-smooth-leave-active {
  transition: opacity 0.3s ease;
}
.fade-smooth-enter-from,
.fade-smooth-leave-to {
  opacity: 0;
}

video-action {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  margin-bottom: 5vw;
  width: 75%;
  height: 8vw;
  background-color: #fff;
  border-radius: 10px;
  padding: 0 10px;

  video-pagination {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    width: 31vw;
    height: 100%;

    button {
      border-radius: 100%;
      width: 5vw;
      height: 5vw;
      overflow: hidden;
      border: #fff solid 0.2vw;
      margin-right: 1vw;
      padding: 0;
      background: #eee;
      flex-shrink: 0;
      position: relative;
      transition: transform 0.2s ease;
      cursor: pointer;

      img {
        width: 10vw;
        height: 10vw;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        object-fit: cover;
      }

      &:hover,
      &.active {
        border: #22bc95 solid 0.2vw;
        transform: scale(1.05);
      }
    }
  }

  video-action-more-btn-container {
    height: 100%;
    width: 24vw;
    display: flex;
    justify-content: center;
    align-items: center;

    button {
      all: unset;
      cursor: pointer;
      background-color: #099471;
      text-align: center;
      color: #fff;
      font-size: 0.8vw;
      border-radius: 2vw;
      width: 6vw;
      height: 2vw;
      transition: all 0.3s ease-in-out;
      display: flex;
      justify-content: center;
      align-items: center;

      .arrow-icon {
        display: inline-block;
        margin-left: 4px;
        transition: transform 0.3s ease;
        transform: rotate(-35deg);
        font-weight: 900;
      }

      &:hover {
        background-color: #19e9b5;
        .arrow-icon {
          transform: rotate(-45deg) translate(2px, -2px);
        }
      }
    }
  }
}

@media screen and (max-width: 840px) {
  video-area-block {
    flex-direction: column;
    padding: 0;
    margin: 5vw 0;

    .video-frame-wrapper {
      width: 100vw;
      height: 56.25vw;
      border-radius: 0;
    }

    video-content {
      width: 90vw;
      height: auto;
      padding: 4vw 0;
      margin: 0 auto;
      h1 {
        display: none;
      }
      video-card {
        background-color: transparent;
        padding: 0;
        align-items: center;
        h2 {
          font-size: 4.5vw;
          text-align: center;
        }
        p {
          font-size: 3.5vw;
          text-align: center;
        }
      }
    }
  }

  video-action {
    flex-direction: column;
    width: 90%;
    height: auto;
    background-color: transparent;

    video-pagination {
      width: 100%;
      justify-content: center;
      margin-bottom: 6vw;
      button {
        width: 12vw;
        height: 12vw;
        margin-right: 3vw;
        img {
          width: 16vw;
          height: 16vw;
        }
      }
    }
    video-action-more-btn-container {
      width: 100%;
      button {
        width: 30vw;
        height: 10vw;
        font-size: 4vw;
        border-radius: 5vw;
      }
    }
  }
}
</style>
