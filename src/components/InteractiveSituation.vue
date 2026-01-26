<script setup>
import { ref } from 'vue'

const MenuIndex = ref(4)
const popIndex = ref(0)

const question = [
  { x: 14, y: 30 },
  { x: 38, y: 40 },
  { x: 77, y: 44 },
]

const Menu = [
  {
    img: 'https://my.tcb-life.com.tw/assets/web_couple_chat-5jsBGiEo.png',
    item: [
      { text: ['我是35歲的阿方，一直很想在台北有個自己的家，但又一直很擔心負擔房貸的風險。'] },
      { text: ['這是我的新婚妻子小梅，她最喜歡清幽舒適的房子，興趣是植栽。'] },
      { text: ['這是我們剛拿到的新屋鑰匙'] },
      {
        text: [
          '沒錯，我們選擇了合庫的房貸壽險，瞬間覺得安心很多。',
          '萬一在貸款期間不幸離開人世，不需要擔心房貸留給珍貴的家人。',
          '而且繳費有多種選擇，非常彈性，大大推薦給也正想買房的你們。',
        ],
        button: { text: '合家幸福定期壽險' },
      },
    ],
  },
  {
    img: 'https://my.tcb-life.com.tw/assets/web_older_chat-qLy6cZCa.png',
    item: [
      { text: ['我是45歲的阿合，工作小有成就的中階主管，但平常要兼顧工作與家庭常讓我心力交瘁。'] },
      {
        text: [
          '這是我最愛的母親，平日因忙於工作，只有假日能陪伴她。',
          '母親最近生病、行動不太方便，需要有人從旁照顧，我經常請假來陪伴她，但是每天移動她上下床讓我的腰也受傷，連去看醫生的時間都沒有。',
          '最近常常在想，母親年紀大了，我是不是該離職專心照顧她….',
        ],
      },
      {
        text: [
          '還好，理專提醒我，合庫人壽的保單可以申請安心守護計劃！',
          '提出申請後，家庭照顧者關懷總會的社工，協助我有效率的照顧安排及申請政府的長照服務。',
          '等待政府核定長照服務期間，還請社工來家中指導我照顧母親的正確方法，讓我不再閃到腰，還分享很多可運用資源，不再因照顧家人而放棄工作了。',
        ],
        button: { text: '安心守護' },
      },
    ],
  },
  {
    img: 'https://my.tcb-life.com.tw/assets/web_travel_chat-BgARif93.png',
    item: [
      {
        text: [
          '我是雪莉，下週準備出發去英國好好放鬆一下！',
          '聽說國外醫療費用超高，萬一旅途中身體不適，醫藥費是不是得自掏腰包，讓旅行變惡夢？',
        ],
      },
      {
        text: [
          '刷卡買機票送的旅平險，好像只保搭飛機這段時間？但下飛機後的旅程才是精華啊！',
          '在倫敦街頭漫步、體驗當地美食，萬一有個閃失怎麼辦？',
        ],
      },
      {
        text: [
          '整理好度假行李箱，為了旅程有完整的人身保障，我會提前在合庫人壽線上投保旅平險。',
          '除了有身故與失能的保障，萬一食物中毒或意外跌倒，也不用擔心高昂的醫療費用，還有24小時海外急難救助諮詢服務，真是令人安心！',
          '想出國的朋友們，快和我一起開啟線上旅平險，讓您的每趟旅程都玩得盡興又安心！',
        ],
        button: { text: '國外旅行平安保險' },
      },
    ],
  },
]
</script>

<template>
  <section>
    <interactive-situation-header>
      <h1>看看可以怎麼保</h1>
      <h2>動手點點小情境互動</h2>
    </interactive-situation-header>
  </section>
  <br /><br /><br />
  <section class="image-wrapper">
    <img
      id="fdss"
      src="https://my.tcb-life.com.tw/assets/storys-BWNGk7Ph.png"
      usemap="#interactive-situation-map"
    />
    <map name="interactive-situation-map" style="cursor: pointer">
      <area shape="rect" coords="0,0,300,500" @click="((MenuIndex = 0), (popIndex = 0))" />
      <area shape="rect" coords="300,0,500,500" @click="((MenuIndex = 1), (popIndex = 0))" />
      <area shape="rect" coords="500,0,900,500" @click="((MenuIndex = 2), (popIndex = 0))" />
    </map>

    <img
      v-for="(item, index) in question"
      class="marker-animation"
      src="data:image/svg+xml,%3csvg%20width='32'%20height='32'%20viewBox='0%200%2032%2032'%20fill='none'%20xmlns='http://www.w3.org/2000/svg'%3e%3ccircle%20cx='15.5'%20cy='15.5'%20r='13.5'%20fill='%23FFBF00'/%3e%3crect%20x='14'%20y='6'%20width='4'%20height='12'%20rx='2'%20fill='white'/%3e%3ccircle%20cx='16'%20cy='23'%20r='2'%20fill='white'/%3e%3c/svg%3e"
      :style="{
        position: 'absolute',
        top: item.y + '%',
        left: item.x + '%',
        zIndex: 1000,
        width: '32px',
        height: '32px',
        cursor: 'pointer',
        transform: 'translate(-50%, -50%)',
      }"
      :key="index"
      @click="((MenuIndex = index), (popIndex = 0))"
    />
  </section>

  <popback @click.self="MenuIndex = 4" v-if="MenuIndex != 4">
    <pop>
      <img class="pop-img" :src="Menu[MenuIndex].img" />
      <buttons>
        <button @click="popIndex = 0" class="active">開始</button>
        <button
          v-for="i in Menu[MenuIndex].item.length - 1"
          :key="i"
          @click="popIndex = i"
          :class="{ active: i <= popIndex }"
        >
          發現{{ i }}
        </button>
        <button
          @click="popIndex = Menu[MenuIndex].item.length"
          :class="{ active: popIndex == Menu[MenuIndex].item.length }"
        >
          完成
        </button>
      </buttons>

      <menu>
        <div v-if="popIndex == 0">
          <div
            style="display: flex; flex-direction: row; align-items: center; justify-content: center"
          >
            <img src="https://my.tcb-life.com.tw/api/assets/7f38b1d9-11ce-4bf2-aca6-d850ba429792" />
            <p>來點點圖片中的驚嘆號吧！</p>
          </div>
        </div>

        <div v-else-if="popIndex != Menu[MenuIndex].item.length">
          <p v-for="(text, tidx) in Menu[MenuIndex].item[popIndex - 1].text" :key="tidx">
            {{ text }}
          </p>
        </div>

        <div v-else>
          <p v-for="(text, tidx) in Menu[MenuIndex].item[popIndex - 1].text" :key="tidx">
            {{ text }}
          </p>
          <button v-if="Menu[MenuIndex].item[popIndex - 1].button" style="margin: 1vw 0">
            {{ Menu[MenuIndex].item[popIndex - 1].button.text }}
          </button>
          <button
            @click="popIndex = 0"
            style="
              background-color: transparent;
              color: #008765;
              border: none;
              margin-top: 10px;
              cursor: pointer;
            "
          >
            重玩一次
          </button>
        </div>
      </menu>
    </pop>
  </popback>
</template>

<style lang="scss" scoped>
@keyframes bounce {
  0%,
  100% {
    transform: translate(-50%, -50%) scale(1);
  }
  50% {
    transform: translate(-50%, -70%) scale(1.1);
  }
}

.marker-animation {
  animation: bounce 2s infinite ease-in-out;
}

.image-wrapper {
  position: relative;
  width: 80%;
  margin: 0 auto;
  @media screen and (max-width: 840px) {
    width: 100%;
  }
}

interactive-situation-header {
  margin-top: 50px;
  position: absolute;
  left: 30%;
  transform: translateX(-50%);
  h1 {
    color: #008765;
    display: inline;
    font-size: 1.5vw;
  }
  h2 {
    color: #008765;
    display: inline;
    font-size: 0.7vw;
    position: relative;
    top: -0.5vw;
  }
  @media screen and (max-width: 840px) {
    left: 20%;
    h1 {
      font-size: 2.5vw;
    }
    h2 {
      font-size: 1.5vw;
    }
  }
}

#fdss {
  width: 100%;
  display: block;
}

popback {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 99998;
  background-color: rgba(0, 0, 0, 0.5);
  pop {
    border-radius: 3vw;
    overflow: hidden;
    position: fixed;
    display: block;
    top: 50%;
    left: 50%;
    height: 90vh;
    width: 90vw;
    z-index: 99999;
    transform: translate(-50%, -50%);
    background-color: #fff;
    buttons {
      z-index: 999999;
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      button {
        background-color: #00000000;
        border: none;
        color: #777;
        font-size: 2.5vw;
        padding: 1vw;
        cursor: pointer;
        &:hover {
          color: #008765e8;
          background-color: #00000022;
        }
        &.active {
          color: #008765;
        }
      }
    }
    .pop-img {
      position: absolute;
      top: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
      z-index: -1;
    }
    menu {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      position: absolute;
      top: 50%;
      right: 5%;
      transform: translateY(-50%);
      height: auto;
      width: 30vw;
      border: #ccc solid 1px;
      border-radius: 3vw;
      background-color: rgb(255, 255, 255);
      padding: 20px;
      box-sizing: border-box;
      p {
        color: #4aae95;
        margin: 0;
        font-size: 1.5vw;
        margin-bottom: 10px;
      }
      button {
        width: 20vw;
        background-color: #008765;
        padding: 1vw;
        border: none;
        position: relative;
        border-radius: 3vw;
        left: 50%;
        transform: translateX(-50%);
        color: #fff;
        cursor: pointer;
      }
    }
  }
}
</style>
