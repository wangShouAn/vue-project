<script setup>
const announcement = [
  {
    p: '【中獎公告】網路投保抽獎活動中獎名單 (合壽15周年慶、小資也能安心保、海外旅遊雙保障)',
    d: '2026-01-20',
    t: [{ text: '活動訊息', color: 'green' }],
  },
  {
    p: '基金合併通知 -「瑞銀(盧森堡)歐洲中型股票基金」(UBS009)及「瑞銀(盧森堡)澳幣基金」(UBS001)',
    d: '2025-12-31',
    t: [{ text: '金融公告', color: 'blue' }],
  },
  {
    p: '【中獎公告】合庫人壽「投資型保險商品保戶回娘家」抽獎活動中獎名單',
    d: '2026-01-02',
    t: [{ text: '活動訊息', color: 'green' }],
  },
]
const news = [
  {
    p: '合庫人壽推出海外旅遊享保障活動  全方位守護好禮加「馬」抽 20',
    d: '2026-01-08',
    t: [{ text: '旅平險', color: 'green' }],
  },
  {
    p: '合庫人壽海外旅遊雙保障活動  提供全方位守護還可抽好禮 ',
    d: '2026-12-24',
    t: [{ text: '旅平險', color: 'green' }],
  },
  {
    p: '合庫人壽攜手合庫銀行  推出「真美傳家」美元利率變動型終身壽險  迎接2026全球經濟新局 2025',
    d: '2025-12-19',
    t: [
      { text: '安心守護', color: 'yellow' },
      { text: '養老保險', color: 'yellow' },
      { text: '利變壽險', color: 'purple' },
    ],
  },
]
</script>
<template>
  <announcement-and-event-container>
    <info-card>
      <h1>公告區</h1>
      <info-card-item v-for="item in announcement">
        <tag v-for="tag in item.t" :class="tag.color">{{ tag.text }}</tag>
        <date> {{ item.d }} </date>
        <p>{{ item.p }}</p>
      </info-card-item>
      <a href="#">看更多-></a>
    </info-card>
    <info-card>
      <h1>新聞稿</h1>
      <info-card-item v-for="item in news">
        <tag v-for="tag in item.t" :class="tag.color">{{ tag.text }}</tag>
        <date> {{ item.d }} </date>
        <p>{{ item.p }}</p>
      </info-card-item>
      <a href="#">看更多-></a>
    </info-card>
  </announcement-and-event-container>
</template>

<style lang="scss" scoped>
announcement-and-event-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  margin-top: 10vw;
  position: relative;
  info-card {
    width: 38vw;
    margin: 0 1vw;
    border-radius: 1vw;
    box-shadow: 0 0 1vw rgba(0, 0, 0, 0.2);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 2vw;
    margin-bottom: 10vw;

    h1 {
      text-align: center;
      font-size: 2vw;
      color: #008e6a;
    }
    info-card-item {
      border-bottom: 1px solid #ccc;
      p {
        margin-top: 1vw;
        font-size: 1.2vw;
        line-height: 1.5;
        white-space: nowrap;
        text-overflow: ellipsis;
        overflow: hidden;
      }
      date {
        font-size: 1.2vw;
        color: #999;
      }
      tag {
        margin-top: 0.5vw;
        display: inline-block;
        font-size: 1.2vw;
        margin-right: 0.5vw;
        color: #fff;
        background-color: #999;
        padding: 0.2vw 0.5vw;
        border-radius: 2vw;
        padding: 0.5vw;
        text-align: center;
        &.green {
          background-color: #008e6a;
        }
        &.blue {
          background-color: #0077be;
        }
        &.yellow {
          background-color: #ffcc00;
        }
        &.purple {
          background-color: #9933cc;
        }
      }
    }
    a {
      display: block;
      text-align: center;
      font-size: 1.5vw;
      margin-top: 2vw;
      color: #fff;
      border-radius: 2vw;
      background-color: #008e6a;
      text-decoration: none;
      width: 8vw;
      margin: 2vw auto 0 auto;
      padding: 0.5vw;
    }
  }
  @media screen and (max-width: 840px) {
    flex-direction: column;
    info-card {
      width: 80%;
      margin: 0 auto;
      margin-bottom: 2vw;
      h1 {
        font-size: 4vw;
      }
      info-card-item {
        p {
          font-size: 3vw;
        }
        date {
          font-size: 3vw;
        }
        tag {
          font-size: 3vw;
        }
      }
      a {
        font-size: 4vw;
        width: 20vw;
        margin-top: 4vw;
      }
    }
  }
}
</style>
