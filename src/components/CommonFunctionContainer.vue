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
  <search-input-container>
    <input type="search" placeholder="我還想查詢.." />
    <img
      src="data:image/svg+xml,%3csvg%20width='24'%20height='24'%20viewBox='0%200%2024%2024'%20fill='none'%20xmlns='http://www.w3.org/2000/svg'%3e%3cpath%20d='M11%2019C15.4183%2019%2019%2015.4183%2019%2011%2019%206.58172%2015.4183%203%2011%203C6.58172%203%203%206.58172%203%2011%203%2015.4183%206.58172%2019%2011%2019Z'%20stroke='%23008E6A'%20stroke-width='2'%20stroke-linecap='round'%20stroke-linejoin='round'/%3e%3cpath%20d='M21.0004%2021L16.6504%2016.65'%20stroke='%23008E6A'%20stroke-width='2'%20stroke-linecap='round'%20stroke-linejoin='round'/%3e%3c/svg%3e"
    />
  </search-input-container>
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
  }
  @media screen and (max-width: 840px) {
    width: 100%;
    button {
      width: 20%;
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
search-input-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0px auto;
  width: 50%;
  padding: 0px 0.2vw;
  height: 30px;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  border: #ccc solid 2px;
  transition: border-color 0.3s ease-in-out;

  &:focus-within {
    border: #05bf90 solid 2px;
  }

  input {
    all: unset;
    width: 100%;
    height: 100%;
    padding: 0 0.5vw;
    border: none;
    border-radius: 5px;
    font-size: 1vw;
  }

  img {
    height: 20px;
    margin-left: 10px;
    cursor: pointer;
  }
  @media screen and (max-width: 840px) {
    width: 80%;
    input {
      font-size: 2vw;
    }
  }
}
</style>
