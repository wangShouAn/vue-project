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
  justify-content: flex-start;
  align-items: stretch;
  gap: 12px;
  margin: 40px auto;
  width: 100%;
  max-width: 1200px;
  padding: 20px;

  button {
    all: unset;
    cursor: pointer;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    width: 200px;
    padding: 1rem;
    background: #ffffff;
    border-radius: 12px;
    box-shadow: 0 10px 10px 0 rgba(0, 0, 0, 0.1);

    img {
      width: 75px;
      height: auto;
      margin-bottom: 0.5rem;
      align-self: center;
    }

    h2 {
      font-size: 3vh;
      margin: 0 0 0.5rem 0;
      color: #333;
      text-align: left;
      width: 100%;
    }

    p {
      font-size: 2vh;
      color: #02020296;
      margin: 0;
      text-align: left;
      line-height: 1.4;
      width: 100%;
    }
  }

  @media screen and (max-width: 1100px) {
    button {
      width: calc(50% - 12px);
    }

    h2 {
      font-size: 3vw;
    }

    p {
      font-size: 2vw;
    }
  }
}

@media screen and (max-width: 480px) {
  button {
    width: 100%;
  }
}
</style>