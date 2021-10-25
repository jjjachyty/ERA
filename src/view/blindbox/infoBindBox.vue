<template>
  <div class="mask">
    <el-dialog :show-close="false" :visible.sync="centerDialogVisible" :width="dialogWidth" center>
      <div class="main">
        <div class="headerTop">
          <img src="../../assets/img/close.png" alt class="close" @click="closemodule" />
        </div>

        <el-row >
          <el-col :xs="24" :md="8" :lg="8" :xl="8">
            <div class="left">
              <img src="@/assets/img/xunzhaung1.png" alt />
              <p>大地原石勛章</p>
            </div>
          </el-col>
          <el-col :xs="24" :md="16" :lg="16" :xl="16">
            <div class="right">
              <div class="info">
                <h6>勛章簡介</h6>
                <p>利用分佈在萊比斯廣袤大陸上的岩石作為材料，由地精工匠打造而成，它通常作為冒險者們首次任務成功的標誌，由萊比斯-ERA酒館公會頒發，價</p>
              </div>
              <div class="count">
                <h6>勛章屬性</h6>
                <div
                  :class="['bj',this.screenWidth >= 600 ?'':'bj600']"
                  :style="`background: url(${bjIMg}) no-repeat center;background-size: contain;`"
                >
                  <div class="item">
                    <img src="@/assets/img/shux1.png" alt />
                    <span>2131</span>
                    <p>總流通量</p>
                  </div>
                  <div class="item">
                    <img src="@/assets/img/shux2.png" alt />
                    <span>普通</span>
                    <p>製造等級</p>
                  </div>
                  <div class="item">
                    <img src="@/assets/img/shux3.png" alt />
                    <span>LV.1</span>
                    <p>稀有等級</p>
                  </div>
                  <div class="item">
                    <img src="@/assets/img/shux4.png" alt />
                    <span>土</span>
                    <p>元素</p>
                  </div>
                </div>
              </div>
            </div>
          </el-col>
        </el-row>
      </div>
    </el-dialog>
  </div>
</template>
<script>
export default {
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      centerDialogVisible: this.show,
      dialogWidth: "0",
      screenWidth: this.GLOBAL.clientWidth,
      bjIMg: require("@/assets/img/shuxbj1.png")
    };
  },
  watch: {
    show(val) {
      this.centerDialogVisible = val;
    }
  },
  created() {},
  mounted() {
    this.setDialogWidth();
  },
  methods: {
    setDialogWidth() {
      if (this.screenWidth < 600) {
        this.dialogWidth = "90%";
        this.bjIMg = require("@/assets/img/shuxbj.png")
      } else {
        this.dialogWidth = 800 + "px";
        this.bjIMg = require("@/assets/img/shuxbj1.png")
      }
    },
    // 点击弹框下的关闭
    closemodule(v) {
      this.$emit("getCancel", v);
    }
  }
};
</script>
<style scoped lang="less">
.main {
  color: #fff;
  padding: 20px 0 0 0;

  .left {
    text-align: center;
    img {
      width: 50%;
    }
    p {
      text-align: center;
      color: #70F4A5;
    }
  }
  .right {
    .info {
      margin-bottom: 10px;
      p {
        font-weight: 800;
        color: #ffffff;
        line-height: 24px;
      }
    }
    h6 {
      margin: 0;
      margin-bottom: 10px;
      color: #70f4a5;
      font-size: 16px;
    }

    .count {
      .bj {
        display: flex;
        justify-content: space-between;
        padding: 20px 40px;
        .item {
          img {
            width: 20px;
            vertical-align: middle;
          }
        }
        span {
          color: #70f4a5;
        }
        p {
          margin: 10px 0;
          text-align: center;
        }
      }
      .bj600{
           padding: 15px 20px;
           p {
          margin: 2px 0;
          text-align: center;
        }
      }
    }
  }
}
.el-dialog--center .el-dialog__body {
  padding: 0;
}

.close {
  width: 25px;
  height: 25px;
  position: absolute;
  right: 26px;
  top: 26px;
}
</style>