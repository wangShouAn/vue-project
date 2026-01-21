<template>
  <popular-events-header>
    <h1>熱門活動</h1>
  </popular-events-header>
  <a id="gf" href="#" style="margin: 5vw 12.5%; width: 75%; position: relative">
    <img
      src="https://my.tcb-life.com.tw/api/assets/b3b9cf03-081c-452a-880c-7596c41b0821"
      style="width: 75%"
    />
    <img
      id="gfr"
      src="https://my.tcb-life.com.tw/api/assets/e089121e-078b-41d1-93b4-0b38c41b9f77"
    />
  </a>
</template>
<style lang="scss" scoped>
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
</style>
