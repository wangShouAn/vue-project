<template>
  <video-area-block>
    <iframe width="724" height="395" src="https://www.youtube.com/embed/fYnGJwbBBIQ" title="🎥 合庫人壽校園巡講精華合輯"
      frameborder="0" allow="
        accelerometer;
        autoplay;
        clipboard-write;
        encrypted-media;
        gyroscope;
        picture-in-picture;
        web-share;
      " referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

    <video-content>
      <h1>影音專區</h1>
      <video-card>
        <h2>合庫人壽校園巡講精華合輯</h2>
        <p>
          風險管理不是害怕未來，而是讓選擇更多、夢想走得更遠。 邀請你一起回顧這段溫暖的校園旅程。
        </p>
      </video-card>
    </video-content>
  </video-area-block>
  <video-action>
    <video-pagination>
      <button>
        <img src="https://img.youtube.com/vi/fYnGJwbBBIQ/hqdefault.jpg" />
      </button>
      <button>
        <img src="https://img.youtube.com/vi/bn0xi52L1QU/hqdefault.jpg" />
      </button>
      <button>
        <img src="https://img.youtube.com/vi/kH3Wyr3lw-Q/hqdefault.jpg" />
      </button>
      <button>
        <img src="https://img.youtube.com/vi/lv6W6-24SRw/hqdefault.jpg" />
      </button>
    </video-pagination>
    <video-action-more-btn-container>
      <button class="lookMore">看更多<span class="arrow-icon">→</span></button>
    </video-action-more-btn-container>
  </video-action>
</template>

<style lang="scss" scoped>
video-area-block {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 4vw auto;
  margin-bottom: 0.5vw;
  padding: 0 16vw;

  iframe {
    width: 31vw;
    height: 17vw;
    border-radius: 1vw;
  }

  .lookMore:hover {
    background-color: #12c397;

    .arrow-icon {
      display: inline-block;
      transition: transform 0.3s ease;
      transform: rotate(-45deg); // 將右箭頭旋轉成右上
      margin-left: 4px;
    }

    &:hover .arrow-icon {
      transform: rotate(-45deg) translate(2px, -2px); // 滑鼠移入時往右上跳動
    }
  }

  video-content {
    height: 17vw;
    width: 24vw;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;

    background-color: #fff;

    h1 {
      font-size: 1.5vw;
      margin: 0;
      padding: 0;
      color: #008765;
    }

    video-card {
      display: flex;
      flex-direction: column;
      border-radius: 1vw;
      background-color: #f6f4ed;
      height: 100%;
      justify-content: center;
      align-items: first baseline;
      padding: 3vw;

      h2 {
        font-size: 0.8vw;
        margin: 0;
        margin-bottom: 1vw;
        padding: 0;
        text-align: left;
      }

      p {
        font-size: 0.7vw;
        margin: 0;
        padding: 0;
      }
    }
  }

  @media screen and (max-width: 840px) {
    flex-direction: column;

    iframe {
      width: 100vw;
      height: 55vw;
    }

    video-content {
      width: 100vw;

      h1 {
        display: none;
      }

      video-card {
        background-color: #ffffff00;

        h2 {
          font-size: 2.5vw;
          position: relative;
          left: 25%;
        }

        p {
          font-size: 1.5vw;
        }
      }
    }
  }
}

video-action {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  margin-bottom: 5vw;
  width: 75%;
  height: 5vw;
  background-color: #fff;
  border-radius: 10px;
  padding: 0 10px;

  video-pagination {
    display: flex;
    justify-content: left;
    align-items: center;
    width: 31vw;
    height: 100%;
    background-color: #fff;
    border-radius: 10px;

    button {
      border-radius: 100%;
      width: 5vw;
      height: 5vw;
      overflow: hidden;
      border: #fff solid 0.2vw;

      img {
        width: 10vw;
        transform: translate(-3vw, -1.5vw);
      }

      &:hover {
        border: #22bc95 solid 0.2vw;
      }
    }

    @media screen and (max-width: 840px) {
      width: 100%;
      height: 15vw;
      justify-content: center;

      button {
        width: 10vw;
        height: 10vw;
        border: #fff solid 0.5vw;

        &:hover {
          border: #22bc95 solid 0.5vw;
        }

        img {
          width: 20vw;
          height: 16vw;
          transform: translate(-7vw, -3vw);
        }
      }
    }
  }

  video-action-more-btn-container {
    height: 100%;
    width: 24vw;

    button {
      all: unset;
      position: relative;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      cursor: pointer;
      margin: 0;
      padding: 0;
      border: none;
      background-color: #099471;
      text-align: center;
      color: #fff;
      font-size: 0.8vw;
      border-radius: 2vw;
      width: 6vw;
      height: 2vw;
      transition: all 0.3s ease-in-out;

      &:hover {
        background-color: #12c397;

        span.arrow {
          display: inline-block;
          transform: rotate(-45deg);
        }
      }
    }

    @media screen and (max-width: 840px) {
      button {
        top: 100%;
        width: 15vw;
        height: 4vw;
        font-size: 2vw;
      }
    }
  }

  @media screen and (max-width: 840px) {
    flex-direction: column;
  }
}
</style>
