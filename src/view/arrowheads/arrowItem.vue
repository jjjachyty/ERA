<template>
  <div class="mask">
    <el-dialog :show-close="false" :visible.sync="centerDialogVisible" :width="dialogWidth" center>
      <div :class="['pcmain',this.screenWidth >= 600 ?'':'main']">
        <div class="headerTop">
          取消算力
          <img src="../../assets/img/close.png" alt class="close" @click="closemodule" />
        </div>
        <div class="Box">
          <div class="money">
            <img src="../../assets/img/arrowIcon.png" alt />
            <div>
              <p>13,253,571</p>
              <span>鎖倉金額（ERA）</span>
            </div>
          </div>
          <div class="tip">7天鎖倉時間結束後不再收取手續費</div>
          <div class="time">
            （剩餘時間：
            <span>120:12:12</span> ）
          </div>
          <div class="list">
            <div class="item">
              <div class="name">手續費：</div>
              <span>200 ERA</span>
            </div>
            <div class="item">
              <div class="name">可收到：</div>
              <span>200 ERA</span>
            </div>
          </div>
          <img src="../../assets/img/arrowQR.png" alt class="submit" />
          <div class="time">注：未滿足鎖倉7天提前取消算力，将扣除鎖倉金額的10%，进入總矿池</div>
        </div>
      </div>
    </el-dialog>
  </div>
</template>
<script>
export default {
  props: {
    showarrowItem: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      centerDialogVisible: this.showarrowItem,
      dialogWidth: "0",
      screenWidth: this.GLOBAL.clientWidth,
      bjIMg: require("@/assets/img/shuxbj1.png")
    };
  },
  watch: {
    showarrowItem(val) {
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
        this.bjIMg = require("@/assets/img/shuxbj.png");
      } else {
        this.dialogWidth = 600 + "px";
        this.bjIMg = require("@/assets/img/shuxbj1.png");
      }
    },
    // 点击弹框下的关闭
    closemodule(v) {
      this.$emit("getCancel", v);
    },
    getConfirmInfo(v) {
      this.$emit("getCancel", v);
    }
  }
};
</script>
<style scoped lang="less">
.pcmain {
  color: #fff;

  .headerTop {
    text-align: center;
    color: #fff;
  }
  .close {
    width: 25px;
    height: 25px;
    position: absolute;
    right: 26px;
    top: 26px;
  }
  .Box {
    .money {
      display: flex;
      justify-content: center;
      align-items: center;
      margin: 32px 0;
      text-align: center;
      img {
        width: 80px;
        margin-right: 20px;
      }
      p {
        color: rgba(112, 244, 165, 1);
        font-size: 30px;
        margin: 0;
      }
    }
    .tip {
      text-align: center;
    }
    .time {
      text-align: center;
      margin-top: 10px;
      span {
        color: rgba(112, 244, 165, 1);
      }
    }
    .list {
      .item {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 20px 0;
        span {
            font-size: 20px;
          color: rgba(112, 244, 165, 1);
        }
      }
    }
    .submit {
      display: block;
      margin: 0 auto;
      width: 60%;
    }
    .zhu {
      text-align: center;
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