<template>
  <section>
    <interactive-situation-header>
      <h1>看看可以怎麼保</h1>
      <h2>動手點點小情境互動</h2>
    </interactive-situation-header>
  </section>
  <br /><br /><br />
  <section>
    <img id="fdss" src="https://my.tcb-life.com.tw/assets/storys-BWNGk7Ph.png" />
  </section>
</template>

<style lang="scss" scoped>
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
  width: 80%;
  position: relative;
  left: 50%;
  transform: translateX(-50%);
  @media screen and (max-width: 840px) {
    width: 100%;
  }
}
</style>
