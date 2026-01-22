<template>
  <div class="video-section-container">
    <div class="main-content-card">
      <div class="video-player-wrapper" @touchstart="handleTouchStart" @touchend="handleTouchEnd">
        <div class="video-slider-track" :style="{ transform: `translateX(-${activeIndex * 100}%)` }">
          <div v-for="(video, index) in videoList" :key="video.id" class="video-slide">
            <div class="video-aspect-box">

              <template v-if="playingIndex !== index">
                <div class="static-poster" @click="startPlay(index)"
                  :style="{ backgroundImage: `linear-gradient(to bottom, rgba(0,0,0,0.3) 0%, transparent 20%, transparent 80%, rgba(0,0,0,0.3) 100%), url(https://img.youtube.com/vi/${video.id}/maxresdefault.jpg)` }">

                  <div class="yt-header-mock">
                    <div class="yt-avatar"></div>
                    <div class="yt-title-text">{{ video.title }}</div>
                    <div class="yt-actions">
                      <div class="yt-icon-watch-later"></div>
                      <div class="yt-icon-share"></div>
                    </div>
                  </div>

                  <div class="play-btn-wrapper">
                    <svg class="yt-play-svg" viewBox="0 0 68 48">
                      <path class="yt-play-bg"
                        d="M66.52,7.74c-0.78-2.93-2.49-5.41-5.42-6.19C55.79,0.13,34,0,34,0S12.21,0.13,6.9,1.55 c-2.93,0.78-4.63,3.26-5.42,6.19C0.06,13.05,0,24,0,24s0.06,10.95,1.48,16.26c0.78,2.93,2.49,5.41,5.42,6.19 C12.21,47.87,34,48,34,48s21.79-0.13,27.1-1.55c2.93-0.78,4.64-3.26,5.42-6.19C67.94,34.95,68,24,68,24S67.94,13.05,66.52,7.74z">
                      </path>
                      <path d="M 45,24 27,14 27,34" fill="#fff"></path>
                    </svg>
                  </div>

                  <div class="yt-bottom-mock">
                    到以下平台觀看： <span class="yt-logo-text">YouTube</span>
                  </div>
                </div>
              </template>

              <template v-else>
                <iframe :src="`https://www.youtube.com/embed/${video.id}?autoplay=1&rel=0&modestbranding=1`"
                  class="video-iframe" allow="autoplay; encrypted-media; fullscreen"></iframe>
              </template>

            </div>
          </div>
        </div>
      </div>

      <div class="info-sidebar">
        <div class="sidebar-header">
          <h2 class="main-title">影音專區</h2>
        </div>
        <div class="sidebar-content">
          <h3 class="video-title">{{ currentVideo.title }}</h3>
          <p class="video-desc">{{ currentVideo.desc }}</p>
        </div>
      </div>
    </div>

    <div class="navigation-bar">
      <div class="thumbnail-list">
        <button v-for="(video, index) in videoList" :key="'t-' + video.id" @click="changeVideo(index)" class="thumb-btn"
          :class="{ 'is-active': activeIndex === index }"
          :style="{ backgroundImage: `url(https://img.youtube.com/vi/${video.id}/mqdefault.jpg)` }"></button>
      </div>
      <button class="more-btn">看更多 <span class="arrow">→</span></button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const videoList = [
  { id: '-qvT8wtz2gA', title: '合庫人壽 一路同行 2025年回顧', desc: '2025 年， 我們不只慶祝 15 週年。' },
  { id: '-s7mmCKrPaY', title: '愛的職務', desc: '當父母離去，面對他們留下的遺物時。' },
  { id: 'fYnGJwbBBIQ', title: '合庫人壽校園巡講', desc: '風險管理讓選擇更多、夢想走得更遠。' },
  { id: 'bn0xi52L1QU', title: '合庫人壽暖心帶領走讀金融街', desc: '合庫人壽喘息學院帶著大家穿越百年時光。' }
];

const activeIndex = ref(0);
const playingIndex = ref(-1);
const touchStartX = ref(0);

const currentVideo = computed(() => videoList[activeIndex.value]);

const changeVideo = (index) => {
  if (activeIndex.value === index) return;
  playingIndex.value = -1; // 切換時恢復靜態圖，消除閃爍
  activeIndex.value = index;
};

const startPlay = (index) => { playingIndex.value = index; };
const handleTouchStart = (e) => { touchStartX.value = e.changedTouches[0].screenX; };
const handleTouchEnd = (e) => {
  const delta = touchStartX.value - e.changedTouches[0].screenX;
  if (Math.abs(delta) > 50) {
    changeVideo(delta > 0 ? (activeIndex.value + 1) % videoList.length : (activeIndex.value - 1 + videoList.length) % videoList.length);
  }
};
</script>

<style lang="scss" scoped>
.video-section-container {
  width: 100%;
  padding: 40px 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: #fafafa;
}

.main-content-card {
  width: 100%;
  max-width: 1000px;
  display: flex;
  flex-direction: column;
  background: #fff;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);

  @media (min-width: 1024px) {
    flex-direction: row;
  }
}

.video-player-wrapper {
  width: 100%;
  background: #000;
  overflow: hidden;
  position: relative;

  @media (min-width: 1024px) {
    width: 65%;
  }
}

.video-slider-track {
  display: flex;
  width: 100%;
  transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1);
  will-change: transform;
}

.video-slide {
  min-width: 100%;
  flex-shrink: 0;
}

.video-aspect-box {
  position: relative;
  width: 100%;
  padding-top: 56.25%;
  background: #000;
}

/* 仿 YouTube 官方 UI 的靜態封面 */
.static-poster {
  position: absolute;
  inset: 0;
  background-size: cover;
  background-position: center;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;

  /* 頂部文字列 */
  .yt-header-mock {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    padding: 12px 15px;
    display: flex;
    align-items: center;
    pointer-events: none;

    .yt-avatar {
      width: 36px;
      height: 36px;
      border-radius: 50%;
      background: #eee;
      margin-right: 12px;
    }

    .yt-title-text {
      color: #fff;
      font-size: 16px;
      font-weight: 500;
      text-shadow: 0 0 2px rgba(0, 0, 0, 0.5);
      flex: 1;
    }
  }

  /* 官方紅色播放鈕 */
  .play-btn-wrapper {
    .yt-play-svg {
      width: 68px;
      height: 48px;
      transition: 0.1s cubic-bezier(0, 0, 0.2, 1);

      .yt-play-bg {
        fill: rgba(33, 33, 33, 0.8);
      }
    }
  }

  &:hover .yt-play-bg {
    fill: #ff0000;
  }

  /* 底部平台提示 */
  .yt-bottom-mock {
    position: absolute;
    bottom: 15px;
    left: 15px;
    background: rgba(0, 0, 0, 0.7);
    color: #fff;
    padding: 8px 15px;
    border-radius: 4px;
    font-size: 14px;

    .yt-logo-text {
      font-weight: bold;
      margin-left: 5px;
    }
  }
}

.video-iframe {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  border: none;
}

/* 其他樣式保持不變 */
.info-sidebar {
  width: 100%;
  background: #f6f4ed;

  @media (min-width: 1024px) {
    width: 35%;
  }

  .sidebar-header {
    padding: 25px 30px 10px;

    .main-title {
      color: #008765;
      font-size: 24px;
    }
  }

  .sidebar-content {
    padding: 0 30px 30px;

    .video-title {
      font-size: 18px;
      font-weight: bold;
      margin-bottom: 10px;
    }

    .video-desc {
      color: #666;
      font-size: 14px;
    }
  }
}

.navigation-bar {
  width: 100%;
  max-width: 1000px;
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.thumbnail-list {
  display: flex;
  gap: 12px;

  .thumb-btn {
    width: 65px;
    height: 65px;
    border-radius: 50%;
    border: none;
    background-size: cover;
    cursor: pointer;
    transition: 0.3s;

    &.is-active {
      box-shadow: 0 0 0 4px #22bc95;
      transform: scale(1.1);
    }
  }
}

.more-btn {
  background: #008765;
  color: #fff;
  padding: 10px 25px;
  border-radius: 30px;
  border: none;
  cursor: pointer;
}
</style>