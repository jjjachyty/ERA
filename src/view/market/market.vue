<template>
  <div :class="['pcmain',this.screenWidth >= 600 ?'':'main']">
    <div class="caintner">
      <el-row>
        <div class="headerMarket">
          <el-col :xs="24" :sm="16" :md="16" :lg="16" :xl="16">
            <div class="nav">
              <img v-if="activeNav==1" src="@/assets/img/paimai.png" alt @click="activeNavmeth(1)" />
              <img
                v-if="activeNav==2"
                src="@/assets/img/paimaino.png"
                alt
                @click="activeNavmeth(1)"
              />

              <img
                v-if="activeNav==2"
                src="@/assets/img/shichang.png"
                alt
                @click="activeNavmeth(2)"
              />
              <img
                v-if="activeNav==1"
                src="@/assets/img/shichangno.png"
                alt
                @click="activeNavmeth(2)"
              />
            </div>
          </el-col>
          <el-col :xs="24" :sm="8" :md="8" :lg="8" :xl="8">
            <div class="navRight" v-if="activeNav==1">
              <el-dropdown trigger="click">
                <span class="el-dropdown-link">
                  拍賣中
                  <!-- <img src="" alt=""> -->
                  <i class="el-icon-arrow-down el-icon--right"></i>
                </span>
                <el-dropdown-menu slot="dropdown">
                  <el-dropdown-item>拍賣中</el-dropdown-item>
                  <el-dropdown-item>已结束</el-dropdown-item>
                </el-dropdown-menu>
              </el-dropdown>
              <el-dropdown trigger="click">
                <span class="el-dropdown-link">
                  最新出價
                  <i class="el-icon-arrow-down el-icon--right"></i>
                </span>
                <el-dropdown-menu slot="dropdown">
                  <el-dropdown-item>最新出价</el-dropdown-item>
                  <el-dropdown-item>最新发布</el-dropdown-item>
                  <el-dropdown-item>时间结束</el-dropdown-item>
                  <el-dropdown-item>最低价格</el-dropdown-item>
                  <el-dropdown-item>最高价格</el-dropdown-item>
                </el-dropdown-menu>
              </el-dropdown>
              <div class="history" @click="history">
                <img src="@/assets/img/pmls.png" alt />
              </div>
            </div>
            <div class="navRight wids" v-if="activeNav==2">
              <el-dropdown trigger="click">
                <span class="el-dropdown-link">
                  最新銷售
                  <!-- <img src="" alt=""> -->
                  <i class="el-icon-arrow-down el-icon--right"></i>
                </span>
                <el-dropdown-menu slot="dropdown">
                  <el-dropdown-item>最新銷售</el-dropdown-item>
                  <el-dropdown-item>最低价格</el-dropdown-item>
                  <el-dropdown-item>最高价格</el-dropdown-item>
                </el-dropdown-menu>
              </el-dropdown>

              <div class="history" @click="historyscls">
                <img src="@/assets/img/scls.png" alt />
              </div>
            </div>
          </el-col>
        </div>
      </el-row>
      <div class="swiper" v-if="this.screenWidth >= 600">
        <div class>
          <swiper :options="swiperOption" @click-slide="clkItem" class="swiper-no-swiping">
            <swiper-slide class="swiper-slide" v-for="(item,index) in carouselArr" :key="index">
              <div class="item">
                <div class="imgItem">
                  <div>100倍</div>
                  <img src="@/assets/img/xunzhaung1.png" class="xz" alt />
                  <p>大地原石勛章 (ID:002101)</p>
                </div>
                <div class="infoItme">
                  <div class="info">
                    <span>最新出價</span>
                    <span class="weight">
                      <img src="@/assets/img/iconMoney.png" alt class="iconMoney" />
                      333,234,567,676
                    </span>
                  </div>
                  <div class="info" v-if="activeNav==1">
                    <span>剩餘時間</span>
                    <span class="weight">12:12:12</span>
                  </div>
                </div>
              </div>
            </swiper-slide>
          </swiper>
          <img
            src="@/assets/img/swiperLeft.png"
            slot="button-prev"
            class="swiper-button-prev swiperLeft"
          />
          <img
            src="@/assets/img/swiperRight.png"
            slot="button-next"
            class="swiper-button-next swiperRight"
          />
        </div>
      </div>
      <div class="main600" v-if="this.screenWidth < 600">
        <el-row>
          <el-col :xs="12" :sm="6" :md="6" :lg="6" :xl="6">
            <div class="item">
              <div class="imgItem">
                <div>100倍</div>
                <img src="@/assets/img/xunzhaung1.png" class="xz" alt />
                <p>大地原石勛章 (ID:002101)</p>
              </div>
              <div class="infoItme">
                <div class="info">
                  <span>最新出價</span>
                  <span class="weight">
                    <img src="@/assets/img/iconMoney.png" alt class="iconMoney" />
                    333,234,567,676
                  </span>
                </div>
                <div class="info" v-if="activeNav==1">
                  <span>剩餘時間</span>
                  <span class="weight">12:12:12</span>
                </div>
              </div>
            </div>
          </el-col>
          <el-col :xs="12" :sm="6" :md="6" :lg="6" :xl="6">
            <div class="item">
              <div class="imgItem">
                <div>100倍</div>
                <img src="@/assets/img/xunzhaung1.png" class="xz" alt />
                <p>大地原石勛章 (ID:002101)</p>
              </div>
              <div class="infoItme">
                <div class="info">
                  <span>最新出價</span>
                  <span class="weight">
                    <img src="@/assets/img/iconMoney.png" alt class="iconMoney" />
                    333,234,567,676
                  </span>
                  <div class="info" v-if="activeNav==1">
                    <span>剩餘時間</span>
                    <span class="weight">12:12:12</span>
                  </div>
                </div>
              </div>
            </div>
          </el-col>
        </el-row>
      </div>
    </div>
    <marketHpList @getConfirmInfoList="getConfirmInfoList" @getCancellist="showList = false" :showList.sync="showList"></marketHpList>

    <marketPMList @getConfirmInfo="getConfirmInfo" @getCancel="show = false" :show.sync="show"></marketPMList>
  </div>
</template>
<script>
import marketPMList from "./marketPMList.vue";
import marketHpList from "./marketHpList.vue";
export default {
  components: {
    marketPMList,
    marketHpList
  },
  data() {
    return {
      screenWidth: this.GLOBAL.clientWidth,
      bannerbjIMg: "@/assets/img/bannerbj600.png",
      activeNav: 1,
      show: false,
      showList:false,
      carouselArr: ["1", "1", "1", "1", "1", "1"],
      swiperOption: {
        //显示分页
        pagination: {
          el: ".swiper-pagination"
        },
        //设置点击箭头
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev"
        },
        //自动轮播
        // autoplay: {
        //   delay: 2000,
        //   //当用户滑动图片后继续自动轮播
        //   disableOnInteraction: false
        // },
        observer: true,
        slidesPerView: 4,
        //开启循环模式
        loop: true
      }
    };
  },
  mounted() {
    this.setDialogWidth();
    console.log(this.screenWidth);
  },
  methods: {
    setDialogWidth() {
      if (this.screenWidth < 600) {
        this.bannerbjIMg = require("@/assets/img/bannerbj.png");
      } else {
        this.bannerbjIMg = require("@/assets/img/bannerbj.png");
      }
    },
    getConfirmInfoList(){

    },
    getConfirmInfo(v) {
      console.log(v);
    },
    //选择提升
    clkItem(index, realIndex) {
      console.log("index = " + index + "; realIndex = " + realIndex);
      this.actives = realIndex;
      if (this.activeNav == 1) {
        this.$router.push({
          path: "/marketInfo",
          query: {
            actives: this.actives
          }
        });
      } else {
        this.$router.push({
          path: "/marketBuyInfo",
          query: {
            actives: this.actives
          }
        });
      }
    },
    activeNavmeth(v) {
      this.activeNav = v;
    },
    history() {
      this.show = true;
    },
    historyscls(){
      this.showList = true;
    }
  }
};
</script>
<style scoped  lang="less">
.pcmain {
  background: rgba(19, 29, 23, 1);
  font-size: 12px;

  .caintner {
    padding: 110px 0 130px;
    max-width: 1970px;
    width: 80%;
    margin: 0 auto;
    .headerMarket {
      .nav {
        margin-top: 10px;
        img {
          width: 50%;
          max-width: 82px;
        }
      }
      .navRight {
        color: #ffffff;
        background: #26352c;
        border-radius: 16px;
        display: flex;
        justify-content: space-around;
        align-items: center;
        text-align: right;
        height: 60px;
        .history {
          width: 100px;
          img {
            width: 100%;
          }
        }
        .el-dropdown-link {
          color: #fff;
        }
      }
      .wids {
        width: 71%;
        float: right;
      }
    }
    .swiper {
      margin: 0 auto;
      position: relative;
      padding: 60px;
      .swiperLeft {
        width: 40px;
        position: absolute;
        right: 0;
        z-index: 999;
      }
      .swiperRight {
        width: 40px;
      }
      .item {
        margin: 0 20px;
        .imgItem {
          background: rgba(38, 53, 44, 1);
          border-radius: 20px;
          padding: 20px 15px;

          div {
            background: rgba(102, 230, 129, 0.33);
            padding: 10px 20px;
            border-radius: 50px;
            text-align: center;
            display: inline-block;
          }
          .xz {
            width: 40%;
            display: block;
            margin: 10px auto;
          }
          p {
            text-align: center;
            margin-top: 30px;
          }
        }
        .infoItme {
          background: rgba(38, 53, 44, 1);
          border-radius: 20px;
          padding: 10px;
          margin-top: 20px;
          .info {
            display: flex;
            justify-content: space-between;
            line-height: 28px;
            img {
              width: 14px;
              vertical-align: middle;
              margin-right: 3px;
            }
            .weight {
              font-weight: 900;
            }
          }
        }
      }
    }
    .main600 {
      margin: 30px auto;

      .item {
        margin: 0 10px;
        .imgItem {
          background: rgba(38, 53, 44, 1);
          border-radius: 20px;
          padding: 20px 15px;
          display: flex;
          flex-flow: column;
          div {
            background: rgba(102, 230, 129, 0.33);
            padding: 10px 20px;
            border-radius: 50px;
            text-align: center;
            display: inline-block;
          }
          .xz {
            width: 40%;
            display: block;
            margin: 10px auto;
          }
          p {
            text-align: center;
            margin-top: 30px;
          }
        }
        .infoItme {
          background: rgba(38, 53, 44, 1);
          border-radius: 20px;
          padding: 10px;
          margin-top: 20px;
          .info {
            display: flex;
            flex-flow: column;
            text-align: center;
            line-height: 28px;
            img {
              width: 14px;
              vertical-align: middle;
              margin-right: 3px;
            }
            .weight {
              font-weight: 900;
            }
          }
        }
      }
    }
  }
}
.main {
  .caintner {
    width: 100%;
    .headerMarket .nav {
      text-align: center;
      margin-top: 0;
      margin-bottom: 30px;
      img {
        width: 40%;
      }
    }
    .headerMarket .navRight {
      width: 94%;
      margin: 0 auto;
    }
  }
}
.el-dropdown-menu__item:hover {
  background: none !important;
  font-weight: 500 !important;
  color: rgba(19, 29, 23, 0.8) !important;
}
</style>