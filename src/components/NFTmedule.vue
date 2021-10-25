<template>
  <div class="mask">
    <el-dialog :show-close="false" :visible.sync="centerDialogVisible" :width="dialogWidth" center>
      <div class="main">
        <div class="headerTop">
          <div class="goback" @click="goback" v-if="avtiveHeader">
            <i class="el-icon-arrow-left"></i>
            我的NFT
          </div>
          {{avtiveHeader?avtiveText:'我的NFT'}}
          <img
            src="../assets/img/close.png"
            alt
            class="close"
            @click="closemodule"
          />
        </div>
        <div v-if="!avtiveHeader">
          <p class="count">NFT數量:0</p>
          <div class="list">
            <div class="tbHeader">
              <span>名字</span>
              <span>身份</span>
              <span>操作</span>
            </div>
            <div class="tbody">
              <div class="dataNo">
                <img src="../assets/img/nodata.png" alt />
                <p class="textNO">暫無數據</p>
              </div>
              <div class="item">
                <div :class="['width1',dialogWidth=='80%'?'width1active':'']">
                  <img src="../assets/img/xunzhaung1.png" alt />
                  <p>泉水琉璃勛章</p>
                </div>
                <div class="width2">200</div>
                <div :class="['width3',dialogWidth=='80%'?'width3active':'']">
                  <img src="../assets/img/paimai.png" alt @click="check(1)" />
                  <img src="../assets/img/ya.png" alt @click="check(2)" />
                </div>
              </div>
            </div>
          </div>
        </div>
        <!-- 質押 -->
        <div class="yabao" v-if="avtiveHeader==2">
          <div class="iconMain">
            <img src="../assets/img/xunzhaung1.png" alt class="iconxunzhang" />
            <div class="boxname">
              <div class="name">泉水琉璃勛章</div>
              <span>ID：002102</span>
            </div>
          </div>
          <div class="textname">算力</div>
          <div class="slcount">
            <span class="slcount">+200</span>
          </div>
          <div class="ntfQR">
            <img src="../assets/img/ntfQR.png" alt />
          </div>
        </div>
        <!-- 拍卖 -->
        <div class="yabao paimai" v-if="avtiveHeader==1">
          <div class="iconMain">
            <img src="../assets/img/xunzhaung1.png" alt class="iconxunzhang" />
            <div class="boxname">
              <div class="name">泉水琉璃勛章</div>
              <span>ID：002102</span>
            </div>
          </div>
          <div class="margin0">
            <div class="textname">起拍價</div>
            <div class="exchange">
              <span class="color">372136129361</span>
              <span>≈ $ 2812</span>
            </div>
          </div>
          <div class="margin0">
            <div class="textname">初始倒計時</div>
            <div class="slcount">
              <span :class="[ time==1? 'bjtime':'']">12小时</span>
              <span :class="[ time==2? 'bjtime':'']">24小时</span>
            </div>
          </div>
          <div class="margin0">
            <div class="textname">
              出價幅度：
              <span class="color">固定加價10%</span>
            </div>
          </div>
          <div class="ntfQR">
            <img src="../assets/img/ntfQR.png" alt />
          </div>
          <div class="rule">
            <h6>注</h6>
            <ul>
              <li>1、注意事項說明注意事項說明注意事項說明，注意事項說明注意事項說明注意事項說明注意事項說明，注意事項說明注意事項說明注意事項說明</li>

              <li>1、注意事項說明注意事項說明注意事項說明，注意事項說明注意事項說明注意事項說明注意事項說明，注意事項說明注意事項說明注意事項說明</li>
            </ul>
          </div>
        </div>
      </div>
    </el-dialog>
  </div>
</template>
<script>
export default {
  props: {
    showNFT: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      centerDialogVisible: this.showNFT,
      dialogWidth: "0",
      avtiveHeader: "", //1是押宝 2 是拍卖
      avtiveText: "",
      time: "1"
    };
  },
  watch: {
    showNFT(val) {
      this.centerDialogVisible = val;
    }
  },
  created() {
    this.setDialogWidth();
  },
  mounted() {
    window.onresize = () => {
      return (() => {
        this.setDialogWidth();
      })();
    };
    this.$nextTick(() => {
      this.setDialogWidth();
    });
  },
  methods: {
    setDialogWidth() {
      var val = document.body.clientWidth;
      const def = 600; // 默认宽度
      if (val < def) {
        this.dialogWidth = "80%";
      } else {
        this.dialogWidth = def + "px";
      }
    },
    goback() {
      this.avtiveText = "";
      this.avtiveHeader = null;
    },
    check(item) {
      this.avtiveHeader = item;
      if (item == 1) {
        this.avtiveText = "拍卖";
      } else {
        this.avtiveText = "質押";
      }

      //选择按钮 押宝 拍卖
      this.$emit("getConfirmNFT", item);
    },
    // 点击弹框下的关闭
    closemodule(v) {
      this.$emit("getCancelNFT", v);
    }
  }
};
</script>
<style scoped lang="less">
.main {
  color: #fff;
}
.el-dialog--center .el-dialog__body {
  padding: 0;
}
.headerTop {
  text-align: center;
  color: #fff;
  position: relative;
  .goback {
    position: absolute;
    left: 0;
    top: 50%;
    transform: translate(0, -50%);
  }
}
.close {
  width: 25px;
  height: 25px;
  position: absolute;
  right: 0;
  top: 50%;
  transform: translate(0, -50%);
}
.count {
  text-align: right;
  margin: 20px 0;
}
.list {
  max-height: 700px;
  .tbHeader {
    display: flex;
    justify-content: space-between;
  }
  .tbody {
    .dataNo {
      text-align: center;
      padding: 30px;
      img {
        margin: 0 auto;
        width: 90px;
        height: 56px;
      }
      .textNO {
        line-height: 20px;
        font-size: 16px;
        padding: 0;
        margin: 0;
      }
    }
    .item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10px;
      .width1 {
        width: 40%;
        text-align: left;
        p {
          display: inline-block;
        }
        img {
          width: 50%;
          max-width: 46px;
          margin: 0;
          padding: 0;
          vertical-align: middle;
        }
      }
      .width1active {
        display: flex;
        align-items: center;
        p {
          width: 50%;
          margin-left: 3%;
        }
      }
      .width2 {
        width: 20%;
        text-align: center;
      }
      .width3 {
        width: 40%;
        text-align: right;
        img {
          width: 35%;
          margin-left: 2%;
          padding: 0;
          vertical-align: middle;
        }
      }
      .width3active {
        width: 40%;
        text-align: right;
        img {
          width: 60%;
          margin-bottom: 2%;
          padding: 0;
          vertical-align: middle;
        }
      }
    }
  }
}

.yabao {
  margin-top: 30px;
  .iconMain {
    display: flex;
    justify-content: center;
    align-items: center;
    .iconxunzhang {
      width: 75px;
    }
    .boxname {
      text-align: center;
      margin-left: 10px;
      .name {
        color: rgba(112, 244, 165, 1);
        font-size: 22px;
      }
    }
  }
  .textname {
    text-align: center; 
  }
  .slcount {
    display: flex;
    justify-content: center;
    span {
      margin: 10px 0;
      padding: 5px 10px;
      background: rgba(102, 230, 129, 0.33);
      text-align: center;
      font-size: 16px;

      border-radius: 20px;
    }
  }
  .ntfQR {
    margin: 20px auto 0;
    width: 80%;
    img {
      width: 100%;
    }
  }
}
.paimai {
  max-height: 400px;
  overflow: scroll;
  .iconMain{
    margin: 20px 0;
  }
  
  .margin0{
    margin-bottom:30px ;
  }
  .slcount {
    justify-content: inherit;
    span {
      margin-right: 10px;
      background: 0;
      padding: 0;
      display: block;
      width: 88px;
      height: 34px;
      line-height: 34px;
    }
    .bjtime {
      background: url(../assets/img/btnBj.png) no-repeat center;
      background-size: cover;
    }
  }
  .textname {
    text-align: left;
    margin-bottom: 10px;
  }
  .exchange {
    background: RGBA(29, 41, 34, 1);
    border-radius: 5px;
    line-height: 60px;
    display: flex;
    justify-content: space-between;
    padding: 0 10px;
    font-size: 18px;
  }
}
.color {
  color: rgba(112, 244, 165, 1);
}
</style>