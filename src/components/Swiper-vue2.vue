<template>
  <div class="swiper" ref="swiper">
    <div
      class="swiper-wrapper"
      :style="'transform: translate3d(' + swiperTransformNum + 'px, 0px, 0px)'"
    >
      <div
        :class="{
          'swiper-slide': true,
          'swiper-slide-prev': swiperCurrIndex === index + 1,
          'swiper-slide-active': swiperCurrIndex === index,
          'swiper-slide-next': swiperCurrIndex === index - 1,
        }"
        v-for="(item, index) in swiperList"
        :key="index"
      >
        <slot :data="item"></slot>
      </div>
    </div>
    <div class="swiper-button-prev" @click="swiperChange(0, true)"></div>
    <div class="swiper-button-next" @click="swiperChange(1, true)"></div>
  </div>
</template>

<script>
import { throttle } from "@/utils/utils";

const DELAYTIME = 5000;
export default {
  name: "swiper",
  props: {
    list: {
      type: Array,
      default: [],
    },
  },
  data() {
    return {
      swiperCurrIndex: 1,
      swiperList: [],
      swiperTransformNum: -930,
    };
  },
  created() {
    const len = this.list.length;
    this.swiperList = Object.freeze([
      this.list[len - 1],
      ...this.list,
      this.list[0],
    ]);
  },
  mounted() {
    const { offsetTop, clientHeight } = this.$refs.swiper;
    const scrollHandler = throttle(() => {
      clearTimeout(this.swiperClickSetTimeOut);
      const navClientHeight =
        document.documentElement.clientHeight || document.body.clientHeight;
      const scrollTop =
        (document.documentElement.scrollTop || document.body.scrollTop) +
        navClientHeight;
      if (
        scrollTop >= offsetTop + clientHeight / 2 &&
        scrollTop <= navClientHeight + clientHeight / 2 + offsetTop
      ) {
        if (this.hasInterval) return;
        this.hasInterval = true;
        this.swiperHandle = setInterval(this.swiperChange, DELAYTIME);
      } else {
        this.hasInterval = false;
        clearInterval(this.swiperHandle);
      }
    }, 500);

    this.$nextTick(scrollHandler);

    window.addEventListener("scroll", scrollHandler);
  },
  methods: {
    swiperChange(status = 1, isClick = false) {
      if (isClick) {
        this.hasInterval = false;
        clearInterval(this.swiperHandle);
        clearTimeout(this.swiperClickSetTimeOut);
        this.swiperClickSetTimeOut = setTimeout(() => {
          this.hasInterval = true;
          this.swiperHandle = setInterval(this.swiperChange, DELAYTIME);
        }, DELAYTIME);
      }
      const maxIndex = this.swiperList.length - 2;
      if (status) {
        this.swiperCurrIndex =
          this.swiperCurrIndex >= maxIndex ? 1 : this.swiperCurrIndex + 1;
        this.swiperTransformNum =
          this.swiperCurrIndex === 1 ? -930 : this.swiperTransformNum - 1010;
      } else {
        this.swiperCurrIndex =
          this.swiperCurrIndex === 1 ? maxIndex : this.swiperCurrIndex - 1;
        this.swiperTransformNum =
          this.swiperCurrIndex === maxIndex
            ? -930 - 1010 * (maxIndex - 1)
            : this.swiperTransformNum + 1010;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.swiper {
  width: 1224px;
  padding: 50px 30px;
  box-sizing: border-box;
  position: relative;
  margin: auto;
  overflow: hidden;
  .swiper-wrapper {
    width: 100%;
    display: flex;
    position: relative;
    .swiper-slide {
      width: 1010px;
      height: 340px;
      overflow: hidden;
      background: #fff;
      box-shadow: 0 6px 25px 0 rgba(230, 230, 230, 0.61);
      position: relative;
      display: flex;
      flex-shrink: 0;
      transform: scale(0.9);
      transition: transform 1s;
      position: relative;
      opacity: 0.8;
    }

    .swiper-slide-prev {
      left: 870px;
      animation: swiperAnimation 1s forwards;
      -webkit-animation: swiperAnimation 1s forwards;
    }

    .swiper-slide-next {
      right: 870px;
      transform: scale(0.9);
      animation: swiperAnimation 1.5s forwards;
      -webkit-animation: swiperAnimation 1.5s forwards;
    }

    .swiper-slide-active {
      position: relative;
      z-index: 100;
      opacity: 1;
      box-shadow: 0 6px 25px 0 rgba(0, 0, 0, 0.6);
      animation: swiperAnimationActive 1.5s forwards;
      -webkit-animation: swiperAnimationActive 1.5s forwards;
    }

    @keyframes swiperAnimation {
      0% {
        transform: scale(1);
      }
      100% {
        transform: scale(0.9);
      }
    }

    @keyframes swiperAnimationActive {
      0% {
        transform: scale(0.9) translateX(200px);
      }
      100% {
        transform: scale(1) translateX(0px);
      }
    }
  }

  .swiper-button-next,
  .swiper-button-prev {
    position: absolute;
    width: 32px;
    height: 32px;
    opacity: 0.5;
    background: #000000;
    border-radius: 2px;
    color: #fff;
    top: calc(50% - 6px);
    cursor: pointer;

    &::after {
      content: " ";
      display: block;
      width: 12px;
      height: 12px;
      margin-left: 10px;
      margin-top: 10px;
      transform: rotate(45deg);
    }
  }

  .swiper-button-prev {
    margin-left: 40px;
    left: 0;

    &::after {
      border-left: 2px solid #fff;
      border-bottom: 2px solid #fff;
    }
  }

  .swiper-button-next {
    margin-right: 40px;
    right: 0;

    &::after {
      border-right: 2px solid #fff;
      border-top: 2px solid #fff;
    }
  }
}
</style>
