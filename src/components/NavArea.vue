<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const logo =
  'https://my.tcb-life.com.tw/assets/%E5%90%88%E5%BA%AB%E4%BA%BA%E5%A3%BDLOGO-BPgS4Q-a.svg'

const navItems = ref([
  {
    open: false,
    name: '保戶服務',
    img: 'https://my.tcb-life.com.tw/api/assets/2a009399-4329-4913-98f4-e7e896c4c17f',
    item: [
      [
        { text: '利率看板', type: 'link' },
        { text: '匯率資訊', type: 'link' },
        { text: '電子單據服務', type: 'link' },
        { text: '行動身分識別身分認證服務', type: 'link' },
        { text: '外來人口「新式統一證號」專區', type: 'link' },
      ],
      [
        { text: '表單下載', type: 'link' },
        { text: '保戶專區', type: 'link' },
        { text: '常見問題', type: 'link' },
        { text: '聯絡我們', type: 'link' },
        { text: '尊享VIP', type: 'link' },
        { text: '合作金庫人壽APP專區', type: 'link' },
      ],
      [
        {
          text: '契約變更作業',
          type: 'title',
          item: [
            { text: '契約變更', type: 'link' },
            { text: '保全聯盟鏈服務', type: 'link' },
          ],
        },
        { text: '保華強制執行專區', type: 'link' },
      ],
    ],
  },
  { open: false, name: '安心守護' },
  {
    open: false,
    name: '所有商品',
    img: 'https://my.tcb-life.com.tw/api/assets/18634038-b350-4491-b36b-ee18adbaea0b',
    item: [
      [
        { text: '熱門商品', type: 'link' },
        { text: '投資型保險', type: 'link' },
        { text: '壽險', type: 'link' },
        { text: '意外傷害保險', type: 'link' },
        { text: '健康醫療保險', type: 'link' },
        { text: '房貸型保險', type: 'link' },
      ],
      [
        { text: '附加與批註條款', type: 'link' },
        { text: '網路投保商品', type: 'link' },
        { text: '電話行銷商品', type: 'link' },
        {
          text: '銀行投保商品',
          type: 'title',
          item: [
            { text: '傳送型商品', type: 'link' },
            { text: '投資型商品', type: 'link' },
            { text: '房貸型商品', type: 'link' },
          ],
        },
      ],
    ],
  },
  {
    open: false,
    name: '公平待客',
    img: 'https://my.tcb-life.com.tw/api/assets/7d15c00b-e668-4e88-a314-64007642b2aa',
    item: [
      [
        {
          text: '公平待客理念',
          type: 'title',
          item: [
            { text: '總經理的話', type: 'link' },
            { text: '公平待客十大原則', type: 'link' },
            { text: '落實公平待客措施', type: 'link' },
          ],
        },
        {
          text: '友善服務',
          type: 'title',
          item: [
            { text: '無障礙網站', type: 'link' },
            { text: '金融友善服務', type: 'link' },
            { text: '友善服務相關訊息', type: 'link' },
          ],
        },
      ],
      [
        {
          text: '感動與成就',
          type: 'title',
          item: [
            { text: '公益活動紀錄', type: 'link' },
            { text: '安心守護', type: 'link' },
            { text: '永續發展', type: 'link' },
          ],
        },
        { text: '樂齡專區', type: 'link' },
        { text: '防詐專區', type: 'link' },
      ],
    ],
  },
  {
    open: false,
    name: '保險知識庫',
    img: 'https://my.tcb-life.com.tw/api/assets/37cf93be-3d13-4f68-becf-b8c9ad76b1c5',
    item: [
      [
        { text: '影音專區', type: 'link' },
        { text: '金融小常識', type: 'link' },
      ],
    ],
  },
  {
    open: false,
    name: '關於我們',
    img: 'https://my.tcb-life.com.tw/api/assets/0a55befe-f8aa-43ce-b8b3-8d63b54807df',
    item: [
      [
        { text: '合作金庫人壽簡介', type: 'link' },
        { text: '首長資料', type: 'link' },
        { text: '得獎紀錄', type: 'link' },
        { text: '信用評價', type: 'link' },
        { text: '聯絡我們', type: 'link' },
        { text: '公益咖啡', type: 'link' },
      ],
      [
        { text: '永續發展', type: 'link' },
        { text: '合作金控', type: 'link' },
        { text: '合作金控永續發展', type: 'link' },
        { text: '法商法國巴黎保險控股公司', type: 'link' },
        { text: '關係企業', type: 'link' },
      ],
    ],
  },
  { open: false, name: '🤔' },
])

function openMenu(index) {
  navItems.value.forEach((item) => {
    item.open = false
  })
  navItems.value[index].open = true
}
function closeMenu() {
  navItems.value.forEach((item) => {
    item.open = false
  })
}

const isVisible = ref(false)

function handleScroll() {
  isVisible.value = window.scrollY > 0
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <nav :class="{ isVisible: !isVisible }">
    <img :src="logo" />
    <ul>
      <li v-for="(item, index) in navItems" :key="index">
        <button @mouseenter="openMenu(index)">
          {{ item.name }}
        </button>
        <menu @mouseleave="closeMenu()" v-if="item.open && item.item">
          <img v-if="item.img" :src="item.img" />

          <ul v-for="(subItems, subIndex) in item.item" :key="subIndex">
            <li v-for="(subItem, i) in subItems" :key="i">
              <a v-if="subItem.type === 'link'" :href="subItem.text">{{ subItem.text }}</a>
              <div v-else-if="subItem.type === 'title'">
                <p>{{ subItem.text }}</p>
                <div>
                  <template v-for="(subSubItem, si) in subItem.item" :key="si">
                    <a>{{ subSubItem.text }} </a>
                    <br />
                  </template>
                </div>
              </div>
            </li>
          </ul>
        </menu>
      </li>
    </ul>
  </nav>
</template>
<style lang="scss" scoped>
nav {
  &.isVisible {
    box-shadow: none;
  }
  transition: all 1s linear;
  box-shadow: 0 0 1vw rgba(0, 0, 0, 0.4);
  width: 75%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 5vw;
  background-color: #fff;
  position: sticky;
  top: 2vw;
  left: 50%;
  z-index: 999;
  margin-top: 1vw;
  border-radius: 4vw;
  transform: translateX(-15%);
  img {
    width: 16vw;
  }
  ul {
    display: flex;
    li {
      list-style: none;
      button {
        overflow: hidden;
        text-align: center;
        white-space: nowrap;
        text-overflow: ellipsis;
        background-color: #fff;
        border: none;
        border-radius: 0.5vw;
        padding: 1vw;
        margin: 0 0.5vw;
        font-size: 1vw;
        cursor: pointer;
        &:hover {
          background-color: #008e6a;
          color: #fff;
        }
      }
      menu {
        box-sizing: border-box;
        overflow-x: scroll;
        display: flex;
        position: fixed;
        width: 80vw;
        height: auto;
        min-height: 30vw;
        top: 5vw;
        left: 50%;
        transform: translateX(-50%);

        background-color: white;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        border-radius: 2vw;
        padding: 2vw;
        img {
          width: 20vw;
          height: 15vw;
          border-radius: 2vw;
        }
        ul {
          display: flex;
          flex-direction: column;

          li {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 1vw 0;
            a {
              width: 15vw;
              color: #000;
              font-size: 1.5vw;
              text-decoration: none;
              &:hover {
                text-decoration: underline;
              }
            }
            div {
              margin: 0;
              padding: 0;
              display: flex;
              flex-direction: column;
              p {
                margin: 0;
                margin-bottom: 2vw;
                padding: 0;
                font-size: 1.5vw;
                color: #000;
              }
              a {
                margin-bottom: 2vw;
                color: #666;
              }
            }
          }
        }
      }
    }
  }
}
</style>
