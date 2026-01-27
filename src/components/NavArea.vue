<script setup>
import { ref, onMounted, onUnmounted, computed, watchEffect } from 'vue'

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
      [
        {
          text: '理賠服務',
          type: 'title',
          item: [
            { text: '保單理賠', type: 'link' },
            { text: '理賠聯盟服務', type: 'link' },
            { text: '理賠醫起通服務', type: 'link' },
          ],
        },
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
])

const isSearchOpen = ref(false)

const isMobile = ref(false)

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
  window.addEventListener('resize', () => {
    isMobile.value = window.innerWidth < 768
  })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  window.removeEventListener('resize', () => {
    isMobile.value = window.innerWidth < 768
  })
})

function toggleSearch() {
  isSearchOpen.value = !isSearchOpen.value
}
</script>

<template>
  <cus-container v-if="!isMobile">
    <div>
      <img
        src="data:image/svg+xml,%3csvg%20width='24'%20height='25'%20viewBox='0%200%2024%2025'%20fill='none'%20xmlns='http://www.w3.org/2000/svg'%3e%3cpath%20fill-rule='evenodd'%20clip-rule='evenodd'%20d='M12%2020.625C12.2875%2020.625%2013.0538%2020.3425%2013.8588%2018.7325C14.2413%2017.9675%2014.5625%2017.02%2014.7863%2015.9375H9.21375C9.4375%2017.02%209.75875%2017.9675%2010.1412%2018.7325C10.9462%2020.3425%2011.7125%2020.625%2012%2020.625ZM8.9425%2014.0625C8.85191%2013.0228%208.85191%2011.9772%208.9425%2010.9375H15.0575C15.1475%2011.9772%2015.1475%2013.0228%2015.0575%2014.0625H8.9425ZM16.6962%2015.9375C16.4163%2017.4675%2015.955%2018.8225%2015.3638%2019.8975C17.1244%2019.0935%2018.5421%2017.69%2019.3638%2015.9375H16.6962ZM19.975%2014.0625H16.9375C17.019%2013.0224%2017.019%2011.9776%2016.9375%2010.9375H19.9737C20.176%2011.9694%2020.176%2013.0306%2019.9737%2014.0625H19.975ZM7.06125%2014.0625H4.025C3.82279%2013.0306%203.82279%2011.9694%204.025%2010.9375H7.0625C6.981%2011.9776%206.981%2013.0224%207.0625%2014.0625H7.06125ZM4.63625%2015.9375H7.30375C7.58375%2017.4675%208.045%2018.8225%208.63625%2019.8975C6.87558%2019.0935%205.4579%2017.69%204.63625%2015.9375ZM9.21375%209.0625H14.7863C14.5625%207.98%2014.2413%207.0325%2013.8588%206.2675C13.0538%204.6575%2012.2875%204.375%2012%204.375C11.7125%204.375%2010.9462%204.6575%2010.1412%206.2675C9.75875%207.0325%209.4375%207.98%209.21375%209.0625ZM16.6962%209.0625H19.3638C18.5421%207.30999%2017.1244%205.90649%2015.3638%205.1025C15.955%206.1775%2016.4163%207.5325%2016.6962%209.0625ZM8.6375%205.1025C8.04625%206.1775%207.585%207.5325%207.305%209.0625H4.63625C5.4579%207.30999%206.87683%205.90649%208.6375%205.1025ZM12%202.5C14.6522%202.5%2017.1957%203.55357%2019.0711%205.42893C20.9464%207.3043%2022%209.84784%2022%2012.5C22%2015.1522%2020.9464%2017.6957%2019.0711%2019.5711C17.1957%2021.4464%2014.6522%2022.5%2012%2022.5C9.34784%2022.5%206.8043%2021.4464%204.92893%2019.5711C3.05357%2017.6957%202%2015.1522%202%2012.5C2%209.84784%203.05357%207.3043%204.92893%205.42893C6.8043%203.55357%209.34784%202.5%2012%202.5Z'%20fill='%23008E6A'/%3e%3c/svg%3e"
      />
      <span>EN</span>
    </div>
    <a href="#">保護專區</a>
    <a href="#">理專專區</a>
  </cus-container>
  <nav :class="{ isVisible: !isVisible }" v-if="!isMobile">
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
                    <a :href="subSubItem.text">{{ subSubItem.text }} </a>
                    <br />
                  </template>
                </div>
              </div>
            </li>
          </ul>
        </menu>
      </li>
      <li>
        <button id="search" @click="toggleSearch">🤔</button>

        <searchMenu v-if="isSearchOpen">
          <h2>關鍵字搜尋</h2>
          <div>
            <input type="text" placeholder="請輸入關鍵字" />
            <button>🤔</button>
          </div>
        </searchMenu>
      </li>
    </ul>
  </nav>

  <nav2 :class="{ isVisible: isVisible }" v-else>
    <button>三</button>
    <img :src="logo" />
    <p></p>
  </nav2>
  <searchback @click.self="toggleSearch" v-if="isSearchOpen" />
</template>
<style lang="scss" scoped>
cus-container {
  div {
    display: flex;
    align-items: center;
  }
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 20vw;
  height: 2vw;
  padding: 1vw;
  border-bottom-left-radius: 1vw;
  border-bottom-right-radius: 1vw;
  color: #008e6a;
  position: sticky;
  top: 0;
  left: 66vw;
  background-color: #d6f0ea;
  z-index: 99999;
  font-weight: bold;
  a {
    color: #008e6a;
    text-decoration: none;
  }
  span {
    margin: 0;
    padding: 0;
  }
}
nav2 {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 8vw;
  background-color: #fff;
  box-shadow: 0 0 1vw rgba(0, 0, 0, 0.4);
  position: sticky;
  top: 1vw;
  left: 0;
  z-index: 9999;
  margin-top: 1vw;
  border-radius: 4vw;
  width: 90vw;
  transform: translateX(2%);

  padding: 0 3vw;
  img {
    width: 25vw;
  }
  p {
    font-size: 1vw;
    color: #000;
    margin: 0;
    margin-left: 1vw;
  }
  button {
    background-color: #00000000;
    border: none;
    font-size: 3vw;
    color: #000;
    margin: 0;
    margin-right: 1vw;
    cursor: pointer;
  }
}
nav {
  &.isVisible {
    box-shadow: none;
    background-color: #00000000;
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
  top: 4vw;
  left: 50%;
  z-index: 9999;
  margin-top: 1vw;
  border-radius: 4vw;
  transform: translateX(-17%);
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
#search {
  &:hover {
    background-color: #00000000;
  }
}
searchMenu {
  padding: 1vw;
  position: absolute;
  display: block;
  top: 5vw;
  width: 35vw;
  transform: translateX(-85%);
  border-radius: 1vw;
  overflow: hidden;
  background-color: #fff;
  border: 1px solid #aaa;
  h2 {
    font-size: 2vw;
    margin: 0;
    margin-bottom: 2vw;
  }
  div {
    position: relative;
  }
  button {
    position: absolute;
    top: 10%;
    right: 0;
    padding: 1vw;
    font-size: 1.5vw;
    background-color: #fff;
    border: none;
    cursor: pointer;
  }
  input {
    all: unset;
    border-radius: 2vw;
    box-sizing: border-box;
    width: 100%;
    padding: 1vw;
    font-size: 1.5vw;
    border: #aaa 1px solid;
    margin-bottom: 1vw;
  }
}
searchback {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 9998;
}
</style>
