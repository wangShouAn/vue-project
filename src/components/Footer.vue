<script setup>
import { ref } from 'vue'

const linkList = [
  {
    text: '網站資訊',
    links: [
      { text: '網站地圖', link: '#' },
      { text: '最新消息', link: '#' },
      { text: '服務據點', link: '#' },
      { text: '常見問題', link: '#' },
      { text: '聯絡我們', link: '#' },
      { text: '無障礙訪問', link: '#' },
    ],
  },
  {
    text: '金融資訊',
    links: [
      { text: '基金通路報酬查詢', link: '#' },
      { text: '金融公告', link: '#' },
      { text: '指定銀行及幣別列表', link: '#' },
    ],
  },
  {
    text: '服務資訊',
    links: [
      { text: '渡假打工青年專區', link: '#' },
      { text: '海外急難諮詢電話', link: '#' },
      { text: '安心守護', link: '#' },
      { text: '因應法定傳染病服務', link: '#' },
      { text: '小額終老專區', link: '#' },
      { text: '保費融資及保單融資專區', link: '#' },
      { text: '保單借款紓困優惠利率專案', link: '#' },
    ],
  },
  {
    text: '企業資訊',
    links: [
      { text: '資訊公開', link: '#' },
      { text: '盡職治理專區', link: '#' },
      { text: '法令公告', link: '#' },
      { text: '公開招標', link: '#' },
      { text: '作業委外概況', link: '#' },
      { text: '保險業經營電子商務自律規範等相關辦法', link: '#' },
      { text: '企業徵才', link: '#' },
    ],
  },
  {
    text: '隱私權專區',
    links: [
      { text: '用戶資料保密措施', link: '#' },
      { text: '個人資料告知事項', link: '#' },
      { text: '網站暨隱私權保護聲明', link: '#' },
      { text: '客戶資料共享之隱私權保護聲明', link: '#' },
    ],
  },
  {
    text: '防詐專區',
    links: [{ text: '防詐專區', link: '#' }],
  },
]

const activeGroups = ref([])

function toggleGroup(title) {
  const index = activeGroups.value.indexOf(title)
  if (index > -1) {
    activeGroups.value.splice(index, 1)
  } else {
    activeGroups.value.push(title)
  }
}

const isOpen = (title) => activeGroups.value.includes(title)
</script>

<template>
  <footer>
    <footer-link-block>
      <img
        src="https://my.tcb-life.com.tw/assets/%E5%90%88%E5%BA%AB%E4%BA%BA%E5%A3%BDLOGO-hrqQj5ac.svg"
      />
      <links>
        <div v-for="linkGroup in linkList" :key="linkGroup.text">
          <h3 @click="toggleGroup(linkGroup.text)">
            {{ linkGroup.text }}
            <span class="mobile-arrow">
              {{ isOpen(linkGroup.text) ? '🔺' : '🔻' }}
            </span>
          </h3>
          <ul :class="{ 'is-open': isOpen(linkGroup.text) }">
            <li v-for="link in linkGroup.links" :key="link.text">
              <router-link :to="link.link">{{ link.text }}</router-link>
            </li>
          </ul>
        </div>
      </links>
      <subscription>
        <h5>快來訂閱獲得最新資訊吧！</h5>
        <input type="email" placeholder="輸入您的信箱" />
        <button class="disabled">訂閱</button>
      </subscription>
    </footer-link-block>
    <socials>
      <span></span>
      <a href="#">
        <img
          src="data:image/svg+xml,%3csvg%20width='40'%20height='41'%20viewBox='0%200%2040%2041'%20fill='none'%20xmlns='http://www.w3.org/2000/svg'%3e%3cg%20clip-path='url(%23clip0_9865_27585)'%3e%3cpath%20d='M0%208.27344C0%203.85516%203.58172%200.273438%208%200.273438H32C36.4183%200.273438%2040%203.85516%2040%208.27344V32.2734C40%2036.6917%2036.4183%2040.2734%2032%2040.2734H8C3.58172%2040.2734%200%2036.6917%200%2032.2734V8.27344Z'%20fill='url(%23paint0_linear_9865_27585)'/%3e%3cpath%20d='M22.7497%2034.3655V22.1216H27.1356L27.7923%2017.3499H22.7496V14.3034C22.7496%2012.9218%2023.159%2011.9804%2025.2733%2011.9804L27.9698%2011.9792V7.71144C27.5034%207.65339%2025.9026%207.52344%2024.0405%207.52344C20.1526%207.52344%2017.4909%209.74712%2017.4909%2013.8309V17.3499H13.0938V22.1216H17.4909V34.3654H22.7497V34.3655Z'%20fill='white'/%3e%3crect%20x='2'%20y='2.27344'%20width='36'%20height='10'%20rx='4'%20fill='url(%23paint1_linear_9865_27585)'/%3e%3cg%20clip-path='url(%23clip1_9865_27585)'%3e%3crect%20y='0.273438'%20width='40'%20height='40'%20fill='%231977F3'/%3e%3cpath%20d='M40%2020.2734C40%209.23047%2031.043%200.273438%2020%200.273438C8.95703%200.273438%200%209.23047%200%2020.2734C0%2030.2539%207.3125%2038.5312%2016.875%2040.0312V26.0547H11.7969V20.2734H16.875V15.8672C16.875%2010.8555%2019.8633%208.08594%2024.4297%208.08594C26.6172%208.08594%2028.9062%208.47656%2028.9062%208.47656V13.3984H26.3828C23.8984%2013.3984%2023.125%2014.9414%2023.125%2016.5234V20.2734H28.6719L27.7852%2026.0547H23.125V40.0312C32.6875%2038.5312%2040%2030.2578%2040%2020.2734Z'%20fill='%231977F3'/%3e%3cpath%20d='M27.7852%2026.0547L28.6719%2020.2734H23.125V16.5234C23.125%2014.9414%2023.8984%2013.3984%2026.3828%2013.3984H28.9062V8.47656C28.9062%208.47656%2026.6172%208.08594%2024.4297%208.08594C19.8633%208.08594%2016.875%2010.8516%2016.875%2015.8672V20.2734H11.7969V26.0547H16.875V40.0312C17.8945%2040.1914%2018.9375%2040.2734%2020%2040.2734C21.0625%2040.2734%2022.1055%2040.1875%2023.125%2040.0312V26.0547H27.7852Z'%20fill='%23FEFEFE'/%3e%3c/g%3e%3c/g%3e%3cdefs%3e%3clinearGradient%20id='paint0_linear_9865_27585'%20x1='16.6667'%20y1='40.2734'%20x2='16.6667'%20y2='0.273437'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%2300C291'/%3e%3cstop%20offset='1'%20stop-color='%23008E6A'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint1_linear_9865_27585'%20x1='22.1468'%20y1='2.27344'%20x2='22.1468'%20y2='12.2734'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='white'%20stop-opacity='0.2'/%3e%3cstop%20offset='1'%20stop-color='white'%20stop-opacity='0'/%3e%3c/linearGradient%3e%3cclipPath%20id='clip0_9865_27585'%3e%3cpath%20d='M0%208.27344C0%203.85516%203.58172%200.273438%208%200.273438H32C36.4183%200.273438%2040%203.85516%2040%208.27344V32.2734C40%2036.6917%2036.4183%2040.2734%2032%2040.2734H8C3.58172%2040.2734%200%2036.6917%200%2032.2734V8.27344Z'%20fill='white'/%3e%3c/clipPath%3e%3cclipPath%20id='clip1_9865_27585'%3e%3crect%20width='40'%20height='40'%20fill='white'%20transform='translate(0%200.273438)'/%3e%3c/clipPath%3e%3c/defs%3e%3c/svg%3e"
        />
      </a>
      <a href="#">
        <img src="https://my.tcb-life.com.tw//assets/youtube-Cz1JTfjx.svg" />
      </a>
      <a href="#">
        <img src="https://my.tcb-life.com.tw/assets/ig-C4vOoGgt.svg" />
      </a>
    </socials>
    <content>
      <div class="footer-text">
        合作金庫人壽保險股份有限公司 版權所有 © 2026 BNP Paribas Cardif TCB Life Insurance Co., Ltd.
        All Rights Reserved 為達最佳顯示效果，本網站建議使用最新版本Google
        Chrome、Edge、Safari、Firefox之瀏覽器
      </div>
      <table class="contact-table">
        <tbody>
          <tr>
            <td>客服電話</td>
            <td>0800-033-133</td>
          </tr>
          <tr>
            <td>客服信箱</td>
            <td>tw_service@tcb-life.com.tw</td>
          </tr>
          <tr>
            <td>客服傳真</td>
            <td>02-2772-7773</td>
          </tr>
          <tr>
            <td>公司地址</td>
            <td>台北市中山區南京東路二段85．87號5樓</td>
          </tr>
        </tbody>
      </table>
    </content>
  </footer>
</template>

<style lang="scss" scoped>
footer {
  box-sizing: border-box;
  background-color: #fff;
  box-shadow: 0px 0 1vw rgba(0, 0, 0, 0.3);
  border-radius: 1vw 1vw 0 0;

  footer-link-block {
    display: flex;
    justify-content: space-around;
    align-items: flex-start;
    padding: 1vw;

    img {
      height: 2vw;
    }

    links {
      margin-left: 1vw;
      display: flex;
      flex-direction: row;
      align-items: flex-start;
      flex-wrap: wrap;

      div {
        margin-right: 2vw;
        width: 10vw;
      }

      h3 {
        font-size: 1.2vw;
        margin-bottom: 0.5vw;
        display: flex;
        justify-content: space-between;
        align-items: center;
      }

      .mobile-arrow {
        display: none;
      }

      ul {
        list-style: none;
        margin: 0;
        padding: 0;

        li {
          margin-bottom: 0.5vw;
          a {
            font-size: 1vw;
            color: #333;
            text-decoration: none;
            &:hover {
              text-decoration: underline;
            }
          }
        }
      }

      @media screen and (max-width: 840px) {
        flex-direction: column;
        width: 100%;

        div {
          width: 100%;
          margin-right: 0;
          border-bottom: #ccc 0.1vw solid;
        }

        h3 {
          font-size: 2.5vw;
          margin: 0;
          padding: 3vw 2vw;
          cursor: pointer;
        }

        .mobile-arrow {
          display: inline-block;
          font-size: 3vw;
        }

        ul {
          display: none;
          padding: 0 4vw 3vw 4vw;

          &.is-open {
            display: block;
          }

          li a {
            font-size: 2vw;
            line-height: 4vw;
          }
        }
      }
    }

    @media screen and (max-width: 840px) {
      padding: 0;
      flex-direction: column;
      align-items: center;

      & > img {
        display: none;
      }
    }
  }
}

subscription {
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  justify-content: baseline;
  align-items: flex-start;
  margin-top: 1vw;

  h5 {
    color: #008e6a;
    font-size: 1.2vw;
    margin-right: 1vw;
    margin-bottom: 1vw;
  }

  input {
    all: unset;
    width: 20vw;
    padding: 0.5vw;
    border: 1px solid #ccc;
    border-radius: 0.5vw;
    font-size: 1vw;
    box-shadow: 0 0.5vw 1vw rgba(0, 0, 0, 0.2);
    &:focus {
      border: 1px solid #008e6a;
    }
  }

  button {
    width: 8vw;
    margin: 2vw 0;
    padding: 0.8vw 1vw;
    border: none;
    border-radius: 3vw;
    background-color: #008e6a;
    color: #fff;
    font-size: 1vw;
    cursor: pointer;
    &:hover {
      background-color: #0cbe91;
    }
    &.disabled {
      background-color: #ccc;
      cursor: not-allowed;
    }
  }

  @media screen and (max-width: 840px) {
    width: 100%;
    padding: 5vw;
    align-items: center;
    h5 {
      font-size: 4vw;
    }
    input {
      width: 80%;
      font-size: 3.5vw;
      padding: 2vw;
    }
    button {
      width: 40%;
      font-size: 3.5vw;
      padding: 2.5vw;
    }
  }
}

socials {
  display: flex;
  margin: 0;
  border-bottom: 0.2vw solid #ccc;
  padding-left: 2vw;
  span {
    width: 2vw;
  }
  img {
    height: 3vw;
    margin-right: 1vw;
    margin-bottom: 1vw;
  }
  @media screen and (max-width: 840px) {
    justify-content: center;
    padding: 3vw 0;
    img {
      height: 8vw;
    }
  }
}

content {
  display: flex;
  flex-direction: row;
  color: #555;
  padding: 2vw;

  .footer-text {
    flex: 1;
    white-space: pre-wrap;
    word-wrap: break-word;
    font-size: 1vw;
    padding-right: 2vw;
  }

  .contact-table {
    width: 40%;
    font-size: 1vw;
    border-collapse: collapse;
    td {
      padding: 0.2vw 0;
    }
  }

  @media screen and (max-width: 840px) {
    flex-direction: column;
    .footer-text {
      font-size: 3vw;
      padding: 2vw 0;
    }
    .contact-table {
      width: 100%;
      font-size: 3vw;
    }
  }
}
</style>
