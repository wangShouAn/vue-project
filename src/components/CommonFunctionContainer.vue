<script></script>
<template>
  <common-function-block>
    <a href="https://www.google.com/">
      <img
        src="https://my.tcb-life.com.tw/api/assets/ae2ec3b4-e3ec-4b5e-9d5b-55fe97a45fc5"
        alt="網路投保"
        draggable="false"
      />
      <p>網路投保</p>
    </a>
    <divider />
    <a>
      <img
        src="https://my.tcb-life.com.tw/api/assets/df0db06d-44f8-42e5-8cc7-8a9baf2108fa"
        alt="電銷商品"
        draggable="false"
      />
      <p>電銷商品</p>
    </a>
    <divider />
    <a>
      <img
        src="https://my.tcb-life.com.tw/api/assets/5c9b3d21-bcad-4ca4-be9f-c0e593eca949"
        alt="保單查詢"
        draggable="false"
      />
      <p>保單查詢</p>
    </a>
    <divider />
    <a>
      <img
        src="https://my.tcb-life.com.tw/api/assets/aa6871c4-3e20-4071-b6e0-f95b0eab2aaf"
        alt="契約變更"
        draggable="false"
      />
      <p>契約變更</p>
    </a>
    <divider />
    <a>
      <img
        src="https://my.tcb-life.com.tw/api/assets/8a411768-6276-489d-8659-46233472f6e7"
        alt="保單理賠"
        draggable="false"
      />
      <p>保單理賠</p>
    </a>
    <divider />
    <a>
      <img
        src="https://my.tcb-life.com.tw/api/assets/d90cd0cc-929d-40c0-be7a-34fa69447037"
        alt="利率看板"
        draggable="false"
      />
      <p>利率看板</p>
    </a>
    <divider />
    <a>
      <img
        src="https://my.tcb-life.com.tw/api/assets/b45e7d96-4201-47af-b680-5fdfbd2b6e67"
        alt="標的專區"
        draggable="false"
      />
      <p>標的專區</p>
    </a>
    <divider />
    <a>
      <img
        src="https://my.tcb-life.com.tw/api/assets/bc967f6b-9084-4229-8fba-49303bd7c0d1"
        alt="表單下載"
        draggable="false"
      />
      <p>表單下載</p>
    </a>
  </common-function-block>
</template>

<style lang="scss" scoped>
common-function-block {
  box-sizing: border-box;
  scale: 0.8;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  margin: 1vw auto auto;
  padding: 1vw;
  background-color: #fff;
  box-shadow: 0 2px 1vw rgba(0, 0, 0, 0.2);
  width: 60%;
  border-radius: 10px;

  a {
    all: unset;
    cursor: pointer;
    box-sizing: border-box;
    margin: auto;

    img {
      transition: all 0.2s ease-in-out;
      height: 5vw;
    }

    &:hover img {
      transform: scale(1.2);
    }
  }

  p {
    margin: 0;
    text-align: center;
    font-size: 1.3vw;
  }

  divider {
    display: inline-block;
    height: 2vw;
    width: 0.2vw;
    background-color: #ccc;
    margin: 0px 1vw;
    @media screen and (max-width: 840px) {
      display: none;
    }
  }
  @media screen and (max-width: 840px) {
    width: 100%;
    a {
      width: 22vw;
      img {
        height: 10vw;
        position: relative;
        left: 25%;
      }
      p {
        font-size: 2vw;
      }
    }
  }
}
</style>
