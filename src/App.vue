<template>
  Vue2:
  <Swiper-vue2 :list="swiperList">
    <template v-slot="{ data: item }">
      <img :src="item.img" class="swiper-slide-img" />
      <div class="swiper-right">
        <div class="swiper-right-content">
          <div class="swiper-name">{{ item.title }}</div>
          <div class="swiper-content">
            <div class="swiper-content-title">商家介绍:</div>
            <div class="swiper-content-content">{{ item.content }}</div>
          </div>
        </div>
        <div class="swiper-info">
          <div class="swiper-info-item" v-if="item.clickNum">
            <div class="swiper-info-item-num">{{ item.clickNum }}</div>
            <div class="swiper-info-item-name">商品日点击人数</div>
          </div>
          <div class="swiper-info-item" v-if="item.consultationTimes">
            <div class="swiper-info-item-num">{{ item.consultationTimes }}</div>
            <div class="swiper-info-item-name">月订单量</div>
          </div>
        </div>
      </div>
    </template>
  </Swiper-vue2>
  Vue3:
  <Swiper-vue3 :list="swiperList">
    <template v-slot="{ data: item }">
      <img :src="item.img" class="swiper-slide-img" />
      <div class="swiper-right">
        <div class="swiper-right-content">
          <div class="swiper-name">{{ item.title }}</div>
          <div class="swiper-content">
            <div class="swiper-content-title">商家介绍:</div>
            <div class="swiper-content-content">{{ item.content }}</div>
          </div>
        </div>
        <div class="swiper-info">
          <div class="swiper-info-item" v-if="item.clickNum">
            <div class="swiper-info-item-num">{{ item.clickNum }}</div>
            <div class="swiper-info-item-name">商品日点击人数</div>
          </div>
          <div class="swiper-info-item" v-if="item.consultationTimes">
            <div class="swiper-info-item-num">{{ item.consultationTimes }}</div>
            <div class="swiper-info-item-name">月订单量</div>
          </div>
        </div>
      </div>
    </template>
  </Swiper-vue3>
</template>

<script setup lang="ts">
import { ref } from "vue";
import SwiperVue2 from "./components/Swiper-vue2.vue";
import SwiperVue3 from "./components/Swiper-vue3.vue";

const swiperList = ref([
  {
    title: "西陇科学股份有限公司",
    content:
      "西陇科学是国内率先上市的化学试剂公司，主要从事化学试剂、诊断试剂、原料药及食品添加剂的研发、生产和销售及基因测序服务，已发展成为国内化学试剂研发能力强、销售覆盖面广、综合配套规模领先的专业制造商和集成供应商。",
    img: "https://staticcdn.youliao.com/static/image/www_pc/index/bussiness-joinUs-1.png",
    clickNum: "1000+",
    consultationTimes: "3500+",
  },
  {
    title: "广州西陇精细化工有限公司",
    content:
      "西陇精细化工是西陇集团旗下化工原料的集成供应商，总部位于广州市，同时是巴斯夫、宝洁、诺力昂、汉姆、SKC、LG、乐天、花王、椰树、索尔维、跃达、中粮、优利德等众多国内外知名品牌的重要合作伙伴和代理商。",
    img: "https://staticcdn.youliao.com/static/image/www_pc/index/bussiness-joinUs-2.png",
    clickNum: "1000+",
    consultationTimes: "3500+",
  },
  {
    title: "山东省冶金科学研究院有限公司",
    content:
      "山冶研究主体业务涉及标准物质研制、第三方检测服务（含金属材料化学成份检测、力学性能检测、材料失效分析、无损检测、计量校准），拥有RMP、ISO/IEC 17025认可、CMA、CAL、PTP等多项资质。",
    img: "https://staticcdn.youliao.com/static/image/www_pc/index/bussiness-joinUs-3.png",
    clickNum: "1000+",
    consultationTimes: "3500+",
  },
  {
    title: "北京鸿润宝顺科技有限公司",
    content:
      "北京鸿润宝顺科技有限公司是一家集研发、生产、销售为一体的现代化高新技术企业。以酪蛋白胨、大豆蛋白胨、酵母浸粉、蛋白胨、胰蛋白胨、牛肉浸粉、酵母膏等培养基原材料和各种培养基为主专业生产经营厂家。",
    img: "https://staticcdn.youliao.com/static/image/www_pc/index/bussiness-joinUs-4.png",
    clickNum: "1000+",
    consultationTimes: "3500+",
  },
  {
    title: "苏州化原化工有限公司",
    content:
      "苏州化原化工有限公司由原国有大中型企业改制而成，主要经营数百种有机类、无机类化工原料。公司自成立以来，一直实行“品种全、价格低、质量优”的化工超市模式，深受数万家客户的青睐。",
    img: "https://staticcdn.youliao.com/static/image/www_pc/index/bussiness-joinUs-5.png",
    clickNum: "1000+",
    consultationTimes: "3500+",
  },
]);
</script>

<style lang="scss" scoped>
.swiper-slide {
  &-img {
    min-width: 420px;
  }

  .swiper-right {
    width: 600px;
    flex-shrink: 0;
    &-content {
      padding: 30px;
    }

    .swiper-name {
      font-size: 18px;
    }

    .swiper-content {
      margin-top: 18px;
      display: flex;
      line-height: 31px;
      &-title {
        width: 250px;
        color: #9195a4;
      }

      &-content {
        color: #666666;
      }
    }

    .swiper-info {
      width: 600px;
      position: absolute;
      bottom: 0;
      height: 100px;
      display: flex;
      align-items: center;
      background: linear-gradient(
        60deg,
        #f5f5f5,
        #f5f5f5 90%,
        #fff 90%,
        #fff 100%
      );

      &-item {
        width: 203px;
        text-align: center;

        &:nth-child(1) {
          position: relative;
          &::after {
            content: "";
            width: 2px;
            height: 20px;
            display: inline-block;
            background: #ececec;
            position: absolute;
            right: 0;
            top: 35%;
          }
        }

        &-num {
          font-size: 36px;
          color: orange;
          font-weight: 550;
          line-height: 40px;
        }

        &-name {
          font-size: 16px;
          color: #999;
        }
      }
    }
  }
}
</style>
