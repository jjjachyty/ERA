<template>
  <div :class="['pcmain',this.screenWidth >= 600 ?'':'main']">
    <div class="caintners">
      <!-- <div class="topimg" v-if="this.screenWidth >= 600" >
        <img src="@/assets/img/bannerarrbig.png" alt class="banner"   />
        <img src="@/assets/img/logo.png" alt class="logo" />
      </div>-->

      <el-row>
        <el-col :xs="24" :sm="8" :md="8" :lg="8" :xl="8">
          <div class="left">
            <!-- :class="['pool', this.screenWidth >= 600?'':'toppoll']" -->
            <div class="pool">
              <div class="title">Angel valley Mining Pool</div>
              <div class="count">23,456,231</div>
              <p class="yu">Remaining prize pool(DXCT) ≈ $6,170,505</p>
              <img src="@/assets/img/logo.png" v-if="this.screenWidth < 600" class="logos" alt />
            </div>

            <div class="rule">
              <div class="poolLeft">
                <div>
                  <span>13,253,571</span>
                  <p>Total Mining Power</p>
                </div>
                <div>
                  <span>13,253,571</span>
                  <p>Total Staked Amount</p>
                </div>
                <div>
                  <span>13,253,571</span>
                  <p>Total Staked Tokens(DXCT) ≈ $9,201,761</p>
                </div>
                <div>
                  <span>13,253,571</span>
                  <p>(DXCT)≈$0</p>
                </div>
              </div>
              <div class="poolRight">
                <div>
                  <span>13,253,571</span>
                  <p>My Mining Power</p>
                </div>
                <div>
                  <span>13,253,571</span>
                  <p>My Staked Amount</p>
                </div>
                <div>
                  <span>13,253,571</span>
                  <p>My Staked Tokens(DXCT)≈ $0</p>
                </div>
                <div class>
                  <img src="@/assets/img/harvest.png" alt />
                </div>
              </div>
            </div>
          </div>
        </el-col>

        <el-col :xs="24" :sm="16" :md="16" :lg="16" :xl="16">
          <div class="right">
            <el-row>
              <el-col
                :xs="12"
                :sm="6"
                :md="6"
                :lg="6"
                :xl="6"
                :key="key"
                v-for="(item,key) in list"
              >
                <div class="contentbox">
                  <div :class="['boxtop' ]">
                    <div class="lefts">Position HashRate：{{key+1}}</div>
                  </div>

                  <img :src="item.icon" alt class="yuansu" />
                  <!-- <span>Confirming…</span> -->
                  <span class="color">Has unlocked +6000 power</span>
                  <div class="info">
                    <img src="@/assets/img/arrowbtn1.png" alt v-if="arrowbtn1" />
                    <img src="@/assets/img/arrowbtn1no.png" alt v-if="!arrowbtn1" />
                    <img src="@/assets/img/arrowbtn2.png" alt @click="qxslz" />
                  </div>
                </div>
              </el-col>
            </el-row>
          </div>
        </el-col>
      </el-row>
    </div>
    <arrowItem
      @getConfirmInfo="getConfirmInfo"
      @getCancel="showarrowItem = false"
      :showarrowItem.sync="showarrowItem"
    ></arrowItem>
    <!-- <arrowUpItem
      @getConfirmUp="getConfirmUp"
      @getCancel="showarrowUp = false"
      :showarrowUp.sync="showarrowUp"
    ></arrowUpItem> -->
  </div>
</template>
<script>
import arrowItem from "./arrowItem.vue";
// import arrowUpItem from "./arrowUpItem.vue";
export default {
  components: {
    arrowItem,
    // arrowUpItem
  },
  data() {
    return {
      screenWidth: this.GLOBAL.clientWidth,
      bannerbjIMg: "@/assets/img/bannerbj600.png",
      showarrowItem: false, //arrowItem
      showarrowUp: false,
      arrowbtn1: false,
      arrowbtn2: true,
      qxslshow: true, //取消算力的显示
      list: [
        {
          bjimh: require("@/assets/img/xzBj1.png"),
          icon: require("@/assets/img/arrowIcon1.png"),
          bei: 100,
          have: 20,
          name: "大地原石勛章"
        },
        {
          bjimh: require("@/assets/img/xzBj1.png"),
          icon: require("@/assets/img/arrowIcon2.png"),
          bei: 100,
          have: 20,
          name: "大地原石勛章"
        },
        {
          bjimh: require("@/assets/img/xzBj1.png"),
          icon: require("@/assets/img/arrowIcon3.png"),
          bei: 100,
          have: 20,
          name: "大地原石勛章"
        },
        {
          bjimh: require("@/assets/img/xzBj1.png"),
          icon: require("@/assets/img/arrowIcon4.png"),
          bei: 100,
          have: 20,
          name: "大地原石勛章"
        },
        {
          bjimh: require("@/assets/img/xzBj1.png"),
          icon: require("@/assets/img/arrowIcon5.png"),
          bei: 100,
          have: 20,
          name: "大地原石勛章"
        },
        {
          bjimh: require("@/assets/img/xzBj1.png"),
          icon: require("@/assets/img/arrowIcon6.png"),
          bei: 100,
          have: 20,
          name: "大地原石勛章"
        },
        {
          bjimh: require("@/assets/img/xzBj1.png"),
          icon: require("@/assets/img/arrowIcon7.png"),
          bei: 100,
          have: 20,
          name: "大地原石勛章"
        },
        {
          bjimh: require("@/assets/img/xzBj1.png"),
          icon: require("@/assets/img/arrowIcon8.png"),
          bei: 100,
          have: 20,
          name: "大地原石勛章"
        }
      ]
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
    getConfirmInfo() {},
    getConfirmUp() {},
    //取消算力值
    qxslz() {
      this.showarrowItem = true;
    },
    //up
    upslz() {
      this.showarrowUp = true;
    }
  }
};
</script>
<style scoped  lang="less">
.pcmain {
  background: rgba(19, 29, 23, 1);
  font-size: 12px;

  .banner {
    max-width: 1970px;
    width: 100%;
    height: 144px;
    margin: 0 auto;
    display: block;
    margin-bottom: 30px;
  }
  .caintners {
    // padding: 140px 0;
    max-width: 1970px;

    margin: 0 auto 0;
    .topimg {
      position: relative;
      .logo {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
      }
    }

    .left {
      //   width: 28%;
      .pool {
        text-align: center;
        padding: 10px 0;
        .title {
          font-size: 24px;
        }

        .count {
          font-size: 40px;
        }
      }
      .rule {
        display: flex;
        justify-content: left;
        background: #26352c;
        border-radius: 16px;
        padding: 12px;
        p {
          margin: 0;
        }
        .poolLeft {
          display: flex;
          flex-direction: column; //修改主轴方向
          flex-wrap: wrap; //开启自动换行
          width: 50%;
          span {
            font-size: 24px;
            font-weight: 800;
          }
          div {
            margin-bottom: 10px;
          }
        }

        .poolRight {
          width: 50%;
          display: flex;
          flex-direction: column; //修改主轴方向
          flex-wrap: wrap; //开启自动换行
          span {
            font-size: 24px;
            font-weight: 800;
            color: #70f4a5;
          }
          div {
            margin-bottom: 15px;
          }
          img {
            width: 60%;
          }
        }
      }
    }
    .right {
      //   width: 70%;
      .contentbox {
        background: #26352c;
        border-radius: 16px;
        display: flex;
        flex-direction: column; //修改主轴方向
        flex-wrap: wrap; //开启自动换行
        padding: 10px 0;
        margin: 0 0 20px 20px;
        font-size: 12px;
        .yuansu {
          width: 30%;
          display: block;
          margin: 5px auto;
        }
        .info {
          display: flex;
          justify-content: center;
          align-items: center;
          img {
            width: 40%;
            margin: 10px 0;
          }
        }

        .boxtop {
          display: flex;
          justify-content: center;
          padding: 0 10px;
          margin-bottom: 5px;
          .lefts {
            height: 30px;
            padding: 0 10px;
            line-height: 30px;
            text-align: center;
            background: rgba(0, 0, 0, 0.4);
            border-radius: 21px;
          }
          .rights {
            height: 30px;
            padding: 0 10px;
            line-height: 30px;
            text-align: center;
            background: rgba(237, 41, 73, 1);
            border-radius: 21px;
          }
        }

        .boxtops2 {
          display: flex;
          justify-content: space-between;
        }

        span {
          margin: 0 auto;
          text-align: center;
        }
        .color {
          color: rgba(112, 244, 165, 1);
          font-size: 12px;
        }
      }
    }
  }
}
.main {
  // padding: 140px 0;
  .caintners {
    width: 95%;

    // padding: 50px 0;
    .left .rule .poolRight span,
    .left .rule .poolLeft span {
      font-size: 18px;
    }
    .left .toppoll {
      position: fixed;
      width: 100%;
      top: 76px;
      z-index: 99;

      background: url("../../assets/img/bannerarrbj.png") no-repeat center;
      background-size: cover;
      .title {
        font-size: 12px;
      }
      .count {
        font-size: 20px;
      }
      .yu {
        font-size: 12px;
        padding: 0;
        margin: 0;
      }
    }
    .logos {
      width: 90px;
      position: absolute;
      left: 10px;
      top: 50%;
      transform: translate(0, -50%);
    }
    .right {
      margin-top: 30px;
      .contentbox {
        margin: 5px;
      }
    }
  }
}
</style>