<script setup>
const product_items = [
  {
    name: '投資型保險',
    img: 'https://my.tcb-life.com.tw/api/assets/272a480d-aefa-49e5-bca4-bc3d25d515f3',
    desc: '一次擁有保險保障與市場投資機會',
  },
  {
    name: '壽險',
    img: 'https://my.tcb-life.com.tw/api/assets/c95adf3f-23b8-481d-aa15-a0860bf7edca',
    desc: '轉嫁死亡風險，提供家人財務未來',
  },
  {
    name: '意外傷害保險',
    img: 'https://my.tcb-life.com.tw/api/assets/4fa16849-eed9-4cfa-b050-8978aade7be2',
    desc: '面對突發意外，多一份保障',
  },
  {
    name: '健康醫療保險',
    img: 'https://my.tcb-life.com.tw/api/assets/614fcce8-08be-4c59-bcc4-a2b2d9a9f07e',
    desc: '健保協同商保，醫療保障更到位',
  },
  {
    name: '房貸型保險',
    img: 'https://my.tcb-life.com.tw/api/assets/a2d0ed5b-ca82-4326-998d-3072526747f8',
    desc: '移轉房貸期間的可能風險，留愛不留債',
  },
]
</script>

<template>
  <div class="product-area-wrapper">
    <button v-for="product in product_items" :key="product.name">
      <img :src="product.img" alt="" />
      <h2>{{ product.name }}</h2>
      <p>{{ product.desc }}</p>
    </button>
  </div>
</template>

<style lang="scss" scoped>
.product-area-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  margin: 10vw auto;
  width: 80%;
  padding: 0;

  border-radius: 10px;

  button {
    position: relative;
    display: block;
    all: unset;
    cursor: pointer;
    box-sizing: border-box;
    margin: 1vw;
    padding: 0.5vw;
    width: 9vw;
    height: 9vw;
    border-radius: 1.2vw;
    box-shadow: 0 2px 1vw rgba(0, 0, 0, 0.2);
    transition: all 0.3s ease-in-out;
    position: relative;

    img {
      width: 3vw;
      position: absolute;
      top: 0;
      left: 50%;
      transform: translateX(-50%);
      margin: 0;
      padding: 0;
    }

    h2 {
      position: absolute;
      top: 30%;
      font-size: 1vw;
      margin: 0;
      padding: 0.5vw;
    }

    p {
      color: #02020296;
      position: absolute;
      top: 60%;
      margin: 0;
      padding: 0;
      font-size: 0.8vw;
    }
  }
  @media screen and (max-width: 840px) {
    justify-content: left;
    align-items: center;
    width: 100%;
    button {
      width: 48vw;
      height: 20vw;
      img {
        width: 10vw;
      }
      h2 {
        padding: 2vw;
        top: 35%;
        font-size: 3vw;
      }
      p {
        margin: 2vw;
        font-size: 2vw;
      }
    }
  }
}
</style>
