<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import SwiperSlide from './components/SwiperSlide.vue'
import CommonFunctionContainer from './components/CommonFunctionContainer.vue'
import SearchInputContainer from './components/SearchInputContainer.vue'
import InteractiveSituation from './components/InteractiveSituation.vue'
import ProductAreaContainer from './components/ProductAreaContainer.vue'

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
    <img src="https://my.tcb-life.com.tw/assets/%E5%90%88%E5%BA%AB%E4%BA%BA%E5%A3%BDLOGO-hrqQj5ac.svg" />

    <item>
      <button @mouseenter="handleMouseEnter(1)" @mouseleave="handleMouseLeave">保戶服務</button>
      <menu @mouseenter="handleMouseEnter(1)" @mouseleave="handleMouseLeave" v-if="menuSeletor === 1"></menu>
    </item>

    <button>安心守護</button>

    <item>
      <button @mouseenter="handleMouseEnter(2)" @mouseleave="handleMouseLeave">所有商品</button>
      <menu @mouseenter="handleMouseEnter(2)" @mouseleave="handleMouseLeave" v-if="menuSeletor === 2"></menu>
    </item>

    <item>
      <button @mouseenter="handleMouseEnter(3)" @mouseleave="handleMouseLeave">公平待客</button>
      <menu @mouseenter="handleMouseEnter(3)" @mouseleave="handleMouseLeave" v-if="menuSeletor === 3"></menu>
    </item>

    <item>
      <button @mouseenter="handleMouseEnter(4)" @mouseleave="handleMouseLeave">保險知識庫</button>
      <menu @mouseenter="handleMouseEnter(4)" @mouseleave="handleMouseLeave" v-if="menuSeletor === 4"></menu>
    </item>

    <item>
      <button @mouseenter="handleMouseEnter(5)" @mouseleave="handleMouseLeave">關於我們</button>
      <menu @mouseenter="handleMouseEnter(5)" @mouseleave="handleMouseLeave" v-if="menuSeletor === 5"></menu>
    </item>

    <search @mouseenter="handleMouseEnter(6)" @mouseleave="handleMouseLeave">🔍</search>
    <menu @mouseenter="handleMouseEnter(6)" @mouseleave="handleMouseLeave" v-if="menuSeletor === 6"></menu>
  </nav>

  <main>
    <section>
      <SwiperSlide />
    </section>

    <section>
      <CommonFunctionContainer />
      <SearchInputContainer />
    </section>
    <InteractiveSituation />
    <section>
      <ProductAreaContainer />
    </section>
    <section>
      <popular-events-header>
        <h1>熱門活動</h1>
      </popular-events-header>
      <a id="gf" href="#" style="margin: 5vw 12.5%; width: 75%; position: relative">
        <img src="https://my.tcb-life.com.tw/api/assets/b3b9cf03-081c-452a-880c-7596c41b0821" style="width: 75%" />
        <img id="gfr" src="https://my.tcb-life.com.tw/api/assets/e089121e-078b-41d1-93b4-0b38c41b9f77" />
      </a>
    </section>
    <section>
      <video-area-block>
        <iframe width="724" height="395" src="https://www.youtube.com/embed/fYnGJwbBBIQ" title="🎥 合庫人壽校園巡講精華合輯"
          frameborder="0" allow="
            accelerometer;
            autoplay;
            clipboard-write;
            encrypted-media;
            gyroscope;
            picture-in-picture;
            web-share;
          " referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

        <video-content>
          <h1>影音專區</h1>
          <video-card>
            <h2>合庫人壽校園巡講精華合輯</h2>
            <p>
              風險管理不是害怕未來，而是讓選擇更多、夢想走得更遠。
              邀請你一起回顧這段溫暖的校園旅程。
            </p>
          </video-card>
        </video-content>
      </video-area-block>
      <video-action>
        <video-pagination>
          <button>
            <img src="https://img.youtube.com/vi/fYnGJwbBBIQ/hqdefault.jpg" />
          </button>
          <button>
            <img src="https://img.youtube.com/vi/bn0xi52L1QU/hqdefault.jpg" />
          </button>
          <button>
            <img src="https://img.youtube.com/vi/kH3Wyr3lw-Q/hqdefault.jpg" />
          </button>
          <button>
            <img src="https://img.youtube.com/vi/lv6W6-24SRw/hqdefault.jpg" />
          </button>
        </video-pagination>
        <video-action-more-btn-container>
          <button>看更多 →</button>
        </video-action-more-btn-container>
      </video-action>
    </section>
    <section>
      <announcement-and-event-container>
        <info-card>
          <h1>公告區</h1>
          <info-card-item>
            <tag> </tag>
            <date> </date>
            <p></p>
          </info-card-item>
        </info-card>
        <info-card>
          <h1>新聞稿</h1>
          <info-card-item> </info-card-item>
        </info-card>
      </announcement-and-event-container>
    </section>
  </main>
  <footer></footer>
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




popular-events-header {
  position: relative;
  left: 20%;
  transform: translateX(-50%);
  transform: translateY(-3vw);

  h1 {
    color: #0e8e6c;
    font-size: 1.5vw;
  }

  @media screen and (max-width: 840px) {
    left: 10%;

    h1 {
      font-size: 2.5vw;
    }
  }
}

#gf {
  #gfr {
    display: none;
  }

  @media screen and (max-width: 840px) {
    img {
      display: none;
    }

    #gfr {
      display: block;
      width: 100%;
    }
  }
}

video-area-block {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 4vw auto;
  margin-bottom: 0.5vw;
  padding: 0 16vw;

  iframe {
    width: 31vw;
    height: 17vw;
    border-radius: 1vw;
  }

  video-content {
    height: 17vw;
    width: 24vw;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;

    background-color: #fff;

    h1 {
      font-size: 1.5vw;
      margin: 0;
      padding: 0;
      color: #008765;
    }

    video-card {
      display: flex;
      flex-direction: column;
      border-radius: 1vw;
      background-color: #f6f4ed;
      height: 100%;
      justify-content: center;
      align-items: first baseline;
      padding: 3vw;

      h2 {
        font-size: 0.8vw;
        margin: 0;
        margin-bottom: 1vw;
        padding: 0;
        text-align: left;
      }

      p {
        font-size: 0.7vw;
        margin: 0;
        padding: 0;
      }
    }
  }

  @media screen and (max-width: 840px) {
    flex-direction: column;

    iframe {
      width: 100vw;
      height: 55vw;
    }

    video-content {
      width: 100vw;

      h1 {
        display: none;
      }

      video-card {
        background-color: #ffffff00;

        h2 {
          font-size: 2.5vw;
          position: relative;
          left: 25%;
        }

        p {
          font-size: 1.5vw;
        }
      }
    }
  }
}

video-action {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  margin-bottom: 5vw;
  width: 75%;
  height: 5vw;
  background-color: #fff;
  border-radius: 10px;
  padding: 0 10px;

  video-pagination {
    display: flex;
    justify-content: left;
    align-items: center;
    width: 31vw;
    height: 100%;
    background-color: #fff;
    border-radius: 10px;

    button {
      border-radius: 100%;
      width: 5vw;
      height: 5vw;
      overflow: hidden;
      border: #fff solid 0.2vw;

      img {
        width: 10vw;
        transform: translate(-3vw, -1.5vw);
      }

      &:hover {
        border: #22bc95 solid 0.2vw;
      }
    }

    @media screen and (max-width: 840px) {
      width: 100%;
      height: 15vw;
      justify-content: center;

      button {
        width: 10vw;
        height: 10vw;
        border: #fff solid 0.5vw;

        &:hover {
          border: #22bc95 solid 0.5vw;
        }

        img {
          width: 20vw;
          height: 16vw;
          transform: translate(-7vw, -3vw);
        }
      }
    }
  }

  video-action-more-btn-container {
    height: 100%;
    width: 24vw;

    button {
      all: unset;
      position: relative;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      cursor: pointer;
      margin: 0;
      padding: 0;
      border: none;
      background-color: #099471;
      text-align: center;
      color: #fff;
      font-size: 0.8vw;
      border-radius: 2vw;
      width: 6vw;
      height: 2vw;
      transition: all 0.3s ease-in-out;
    }

    @media screen and (max-width: 840px) {
      button {
        top: 100%;
        width: 15vw;
        height: 4vw;
        font-size: 2vw;
      }
    }
  }

  @media screen and (max-width: 840px) {
    flex-direction: column;
  }
}
</style>
