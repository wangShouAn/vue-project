<template>
  <div class="video-section-outer">
    <div class="content-container">
      <div class="video-layout-grid">

        <div class="header-area">
          <div class="title-wrapper">
            <h2 class="section-title">影音專區</h2>
          </div>
        </div>

        <div class="video-cell">
          <div class="video-wrapper">
            <div class="slider-track" :style="{ transform: `translateX(-${activeIndex * 100}%)` }">
              <div v-for="(video, index) in videoList" :key="video.id" class="slide-item">
                <div class="video-ratio-box">
                  <template v-if="playingIndex !== index">
                    <div class="video-poster" @click="startPlay(index)" :style="{
                      backgroundImage: `url(https://img.youtube.com/vi/${video.id}/maxresdefault.jpg)`,
                    }">
                      <div class="play-btn-wrapper">
                        <svg viewBox="0 0 68 48" class="custom-play-svg">
                          <path fill="#f00"
                            d="M66.5 7.7c-.8-2.9-2.5-5.4-5.4-6.2C55.8.1 34 0 34 0S12.2.1 6.9 1.5c-2.9.8-4.6 3.3-5.4 6.2C0 13 0 24 0 24s0 11 1.5 16.3c.8 2.9 2.5 5.4 5.4 6.2 5.3 1.4 27.1 1.5 27.1 1.5s21.8-.1 27.1-1.5c2.9-.8 4.6-3.3 5.4-6.2C68 35 68 24 68 24s0-11-1.5-16.3z" />
                          <path fill="#fff" d="M45 24L27 14v20z" />
                        </svg>
                      </div>
                    </div>
                  </template>
                  <template v-else>
                    <iframe :src="`https://www.youtube.com/embed/${video.id}?autoplay=1`" class="iframe-fit"
                      allow="autoplay; fullscreen"></iframe>
                  </template>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="content-area">
          <div class="beige-card">
            <div class="card-inner">
              <h3 class="v-title">{{ currentVideo.title }}</h3>
              <p class="v-desc">{{ currentVideo.desc }}</p>
            </div>
          </div>
        </div>

        <div class="footer-cell">
          <div class="footer-flex-row">
            <div class="thumb-group">
              <button v-for="(video, index) in videoList" :key="video.id" @click="changeVideo(index)" class="dot"
                :class="{ active: activeIndex === index }" :style="{
                  backgroundImage: `url(https://img.youtube.com/vi/${video.id}/mqdefault.jpg)`,
                }"></button>
            </div>
            <button class="more-link" @click="goToMore">看更多 ↗</button>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

const videoList = [
  { id: '-qvT8wtz2gA', title: '合庫人壽 一路同行 2025年回顧', desc: '2025 年， 我們不只慶祝 15 週年， 更用行動，陪伴每一段人生。' },
  { id: '-s7mmCKrPaY', title: '愛的職務', desc: '當父母離去，面對他們留下的遺物時，你會想起他們扮演的哪一個角色？' },
  { id: 'fYnGJwbBBIQ', title: '合庫人壽校園巡講精華合輯', desc: '風險管理不是害怕未來，而是讓選擇更多、夢想走得更遠。' },
  { id: 'bn0xi52L1QU', title: '合庫人壽暖心帶領走讀金融街', desc: '合庫人壽喘息學院帶著家庭照顧者「走讀台中金融街」一同穿越百年時光。' },
  { id: 'xJV69s_OSXM', title: '【Ｎ１文法】～たためしがない', desc: '學問好比腸胃裡的食物，裝下多少並不重要，吸收多少才重要' },
]

const activeIndex = ref(0)
const playingIndex = ref(-1)
const currentVideo = computed(() => videoList[activeIndex.value] || videoList[0])

const startPlay = (index: number) => {
  activeIndex.value = index
  playingIndex.value = index
}

const changeVideo = (index: number) => {
  activeIndex.value = index
  playingIndex.value = -1
}

const goToMore = () => {
  window.location.href = 'https://my.tcb-life.com.tw/video'
}
</script>

<style lang="scss" scoped>
// 定義變數
$primary-green: #008765;
$hover-green: #27d4a9;
$button-green: #189072;
$active-border: #22bc95;
$bg-beige: #f8f6f2;
$white: #fff;
$black: #000;

$transition-base: 0.3s ease;
$transition-slider: 0.6s cubic-bezier(0.4, 0, 0.2, 1);
$shadow-light: 0 10px 30px rgba(0, 0, 0, 0.1);

// 定義混入 (Mixins)
@mixin flex-center {
  display: flex;
  align-items: center;
  justify-content: center;
}

@mixin absolute-full {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

// 樣式主體
.video-section-outer {
  width: 100%;
  padding: 60px 0;
  background: $white;
  @include flex-center;
  overflow: hidden;
}

.content-container {
  width: 90%;
  max-width: 1100px;
}

.video-layout-grid {
  display: grid;
  grid-template-columns: 60% 40%;
  align-items: end;
  width: 100%;

  @media (max-width: 1050px) {
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}

// 標題區域
.header-area {
  grid-column: 2;
  margin-bottom: 20px;

  @media (max-width: 1050px) {
    order: 1;
    text-align: center;
  }

  .title-wrapper {
    padding-left: 150px;
    margin-bottom: -80px;

    @media (max-width: 1050px) {
      padding-left: 0;
    }

    .section-title {
      color: $primary-green;
      font-size: 32px;
      font-weight: bold;

      @media (max-width: 1050px) {
        margin-bottom: 80px;
        padding-right: 500px;
      }
    }
  }
}

// 影片顯示區
.video-cell {
  grid-column: 1;
  grid-row: 2;
  z-index: 5;
  width: 100%;

  @media (max-width: 1050px) {
    order: 2;
  }

  .video-wrapper {
    width: 100%;
    border-radius: 15px 15px 0 15px;
    overflow: hidden;
    background: $black;
    box-shadow: $shadow-light;

    .slider-track {
      display: flex;
      transition: transform $transition-slider;
      width: 100%;

      .slide-item {
        min-width: 100%;
      }
    }
  }
}

.video-ratio-box {
  position: relative;
  width: 100%;
  height: 0;
  padding-bottom: 56.25%;

  .video-poster,
  .iframe-fit {
    @include absolute-full;
    object-fit: cover;
  }

  .video-poster {
    background-size: cover;
    background-position: center;
    @include flex-center;
    cursor: pointer;

    .play-btn-wrapper {
      width: 68px;
      height: 48px;
      z-index: 10;
      filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.3));

      .custom-play-svg {
        width: 100%;
        height: 100%;
      }
    }
  }
}

// 文字內容區
.content-area {
  grid-column: 2;
  grid-row: 2;

  @media (max-width: 1050px) {
    order: 3;
  }

  .beige-card {
    background: $bg-beige;
    border-radius: 0 20px 20px 0;
    margin-left: -60px;
    padding: 40px 40px 40px 100px;
    min-height: 200px;
    display: flex;
    align-items: center;

    @media (max-width: 1050px) {
      margin: -20px 0 0 0;
      padding: 40px 20px;
      border-radius: 20px;
      text-align: center;
      min-height: 20px;
      justify-content: center;
      background-color: $white;
    }

    .v-title {
      font-size: 1.25rem;
      margin-bottom: 10px;
    }

    .v-desc {
      color: #666;
      line-height: 1.6;
    }
  }
}

// 底部控制區
.footer-cell {
  grid-column: 1 / span 2;
  padding-top: 40px;

  @media (max-width: 1050px) {
    order: 4;
  }

  .footer-flex-row {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    gap: 45%;
    width: 100%;

    @media (max-width: 1050px) {
      flex-direction: column;
      gap: 20px;
    }
  }
}

.thumb-group {
  display: flex;
  gap: 15px;
  flex-wrap: wrap;
  justify-content: center;

  .dot {
    width: 65px;
    height: 65px;
    border-radius: 50%;
    background-size: cover;
    background-position: center;
    border: 3px solid transparent;
    cursor: pointer;
    transition: $transition-base;

    &.active {
      border-color: $active-border;
      transform: scale(1.1);
    }

    &:hover:not(.active) {
      opacity: 0.8;
    }
  }
}

.more-link {
  background: $button-green;
  color: $white;
  border: none;
  padding: 12px 35px;
  border-radius: 30px;
  font-weight: bold;
  cursor: pointer;
  transition: background $transition-base;

  &:hover {
    background: $hover-green;
  }
}
</style>