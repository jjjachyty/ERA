<template>
  <div id="app">
    <div :class="[navBarFixed == true ? 'navBarWrap' :'','header']">
      <el-col :xs="12" :sm="6" :md="4" :lg="3" :xl="8">
        <img
          :class="['logoimg',this.screenWidth >= 600 ?'':'logoimg600']"
          src="./assets/img/logo.png"
          alt="logo"
        />
      </el-col>
      <el-col :xs="12" :sm="18" :md="18" :lg="20" :xl="20">
        <div v-if="Object.keys(rightNavItems).length === 0?true:false" class="box">
          <!-- <el-menu
            :default-active="defaultOpenedsIndex"
            id="navid"
            class="nav"
            mode="horizontal"
            :default-openeds="defaultOpeneds"
            router
          >-->
          <el-menu
            @select="handleSelect"
            id="navid"
            mode="horizontal"
            :default-openeds="defaultOpeneds"
            default-active="/home"
            class="nav"
          >
            <!-- <el-menu-item
              :key="key"
              v-for="(item,key) in leftNavItems"
              :index="item.index"
              :route="item.activeIndex"
             
            >{{item.name}}</el-menu-item>-->
            <el-menu-item
              :key="key"
              v-for="(item,key) in leftNavItems"
              :index="item.activeIndex"
            >{{item.name}}</el-menu-item>
            <!-- <el-submenu
          style="float:right;"
          class="right-item"
          v-if="Object.keys(rightNavItems).length === 0?false:true"
          index="10"
        >
          <template slot="title">
            <i class="el-icon-s-fold" style="font-size:28px;"></i>
          </template>
          <el-menu-item
            :key="key"
            v-for="(item,key) in rightNavItems"
            :index="item.index"
            :route="item.activeIndex"
          >{{item.name}}</el-menu-item>
            </el-submenu>-->
          </el-menu>
          <div class="navimg" >
            <img src="./assets/img/en.png" alt class="luange" />
            <div @mouseenter="enter" v-if="!mypackage">
              <img
                src="./assets/img/package.png"
                alt
                class="package"
                v-if="mouse"
                @click="linkShow"
              />
              <img
                src="./assets/img/packageenter.png"
                @mouseout="out"
                alt
                class="package"
                v-if="!mouse"
                @click="linkShow"
              />
            </div>
            <div @mouseenter="enter" v-if="mypackage">
              <img
                src="./assets/img/mypackage.png"
                alt
                class="package"
                v-if="mouse"
                @click="linkPackageShow"
              />
              <img
                src="./assets/img/mypackageenter.png"
                @mouseout="out"
                alt
                class="package"
                v-if="!mouse"
                @click="linkPackageShow"
              />
            </div>
          </div>

          <div class="item">
            <img :src="item.img" alt v-for="(item,key) in navImg" :key="key" />
          </div>
        </div>

        <img
          class="navs"
          @click="drawer = true"
          v-if="Object.keys(rightNavItems).length === 0?false:true"
          src="./assets/img/navlist.png"
        />
      </el-col>
    </div>
    <el-drawer :visible.sync="drawer" :size="size" :with-header="false">
      <div class="navimgList">
        <img src="./assets/img/en.png" alt class="luange" />
        <img src="./assets/img/package.png" v-if="!mypackage" alt class="package" @click="linkShow" />
        <img
          src="./assets/img/mypackage.png"
          alt
          class="package"
          v-if="mypackage"
          @click="linkPackageShow"
        />
      </div>
      <div class="navList">
        <!-- <el-menu
          :default-active="defaultOpenedsIndex"
          id="navid"
          class="nav"
          mode="horizontal"
          :default-openeds="defaultOpeneds"
          router
        >-->
        <el-menu
          @select="handleSelect"
          id="navid"
          mode="horizontal"
          :default-openeds="defaultOpeneds"
          default-active="/home"
          class="nav"
        >
          <el-menu-item
            :key="key"
            v-for="(item,key) in rightNavItems"
            :index="item.activeIndex"
          >{{item.name}}</el-menu-item>
          <!-- <el-menu-item
            :key="key"
            v-for="(item,key) in rightNavItems"
            :index="item.index"
            :route="item.activeIndex"
          >{{item.name}}</el-menu-item>-->
        </el-menu>
      </div>
      <div class="itemList">
        <img :src="item.img" alt v-for="(item,key) in navImg" :key="key" />
      </div>
    </el-drawer>
    <linkPackage @getConfirm="getConfirmCheck" @getCancel="show = false" :show.sync="show"></linkPackage>

    <NFTmedule
      @getConfirmNFT="getConfirmNFT"
      @getCancelNFT="showNFT = false"
      :showNFT.sync="showNFT"
    ></NFTmedule>
    <router-view></router-view>
  </div>
</template>

<script>
import NFTmedule from "./components/NFTmedule.vue";
import linkPackage from "./components/linkPackage.vue"; // 第一步 先使用import导入你要在该组件中使用的子组件
import {getContract} from "@/assets/js/web3.js"
export default {
  name: "App",
  components: {
    linkPackage,
    NFTmedule
  },
  data() {
    return {
      screenWidth: document.body.clientWidth,
      navItems: [
        { name: "Home", activeIndex: "/home", index: "1" },
        { name: "NFT", activeIndex: "/blindbox", index: "2" },
        { name: "Market", activeIndex: "/market", index: "3" },
        // { name: "Pledge Mining", activeIndex: "/arrowheads", index: "4" },
        { name: "Farms", activeIndex: "/FARMS", index: "4" }
        // { name: "Contract" },
        // { name: "Backstage" }
      ],
      defaultOpenedsIndex: "1",
      defaultOpeneds: null,
      navBarFixed: false,
      drawer: false,
      size: "200px",
      show: false, //链接钱包弹窗
      showNFT: false, //NFT
      mouse: true, //鼠标滑过
      mypackage: true,
      navImg: [
        {
          img: require(`@/assets/img/navRight1.png`),
          link: ""
        },
        {
          img: require(`@/assets/img/navRight2.png`),
          link: ""
        },
        {
          img: require(`@/assets/img/navRight3.png`),
          link: ""
        },
        {
          img: require(`@/assets/img/navRight4.png`),
          link: ""
        }
      ]
    };
  },
  computed: {
    leftNavItems: function() {
      return this.screenWidth >= 600 ? this.navItems : {};
    },
    rightNavItems: function() {
      return this.screenWidth < 600 ? this.navItems : {};
    }
  },
  mounted() {
    window.onresize = () => {
      this.screenWidth = document.body.clientWidth;
      this.GLOBAL.clientWidth = this.screenWidth;
    };
    this.$nextTick(() => {
      this.screenWidth = document.body.clientWidth;
      this.GLOBAL.clientWidth = this.screenWidth;
    });
    this.activeNav();
    // 事件监听滚动条
    window.addEventListener("scroll", this.watchScroll);
  },
  watch: {
    $route(to, from) {
      this.activeNav();
    },
    screenWidth(newValue) {
      // 为了避免频繁触发resize函数导致页面卡顿，使用定时器
      if (!this.timer) {
        // 一旦监听到的screenWidth值改变，就将其重新赋给data里的screenWidth
        this.screenWidth = newValue;
        this.GLOBAL.clientWidth = this.screenWidth;
        this.timer = true;
        setTimeout(() => {
          //console.log(this.screenWidth);
          this.timer = false;
        }, 400);
      }
    }
  },
  methods: {
    activeNav() {
      let path = this.$route.path;
      let thisNav = this.navItems.find(item => {
        return item.activeIndex.includes(path);
      });
      if (thisNav) {
        this.defaultOpeneds = [thisNav.index];
        this.defaultOpenedsIndex = thisNav.index;
        this.GLOBAL.clientWidth = this.screenWidth;
      }
    },
    handleSelect(key, keyPath) {
      if (key) {
        this.$router.push({
          path: key,
          params: { data: "query" }
        });
      }
    },
    watchScroll() {
      var scrollTop =
        window.pageYOffset ||
        document.documentElement.scrollTop ||
        document.body.scrollTop;
      //  当滚动超过 50 时，实现吸顶效果
      if (scrollTop > 49) {
        this.navBarFixed = true;
      } else {
        this.navBarFixed = false;
      }
    },
    //获取钱包链接选择
    getConfirmCheck(v) {
      console.log(v);
    },
    //我的钱包
    linkPackageShow() {
      // this.show = true
      this.showNFT = true;
      getContract().then(()=>{
        alert("钱包连接成功")
      }).catch(err=>{
        alert("连接metamask 出错",err)
      })
    },
    //链接钱包
    linkShow() {
      this.show = true

    },
    //NFT方法
    getConfirmNFT(v) {},

    enter() {
      this.mouse = false;
    },
    out() {
      this.mouse = true;
    }
  }
};
</script>

<style >
@import "./assets/font/font.css";
#app {
  color: #fff;
  font-family: "Futura-Book-2";
  background: rgba(19, 29, 23, 1);
}
#app div {
  font-family: "Gen2";
}
/* .pcmain{
  min-height: 100vh;
} */
.header {
  width: 100%;
  z-index: 999;
  padding: 20px 0;
  position: fixed;
  top: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.el-menu {
  background: 0;
}
.logoimg {
  width: 70%;
  margin-left: 10%;
}
.logoimg600 {
  width: 40%;
  margin-left: 10%;
}
.el-menu.el-menu--horizontal {
  border: 0 !important;
  border-bottom: 0 !important;
  background: 0 !important;
}
.box .el-menu--horizontal > .el-menu-item.is-active {
  border-bottom: 0 !important;
  font-size: 18px;
  color: #70f4a5 !important;
  position: relative;
}
.box .el-menu--horizontal > .el-menu-item.is-active::after {
  background: #70f4a5 !important;
  content: "";
  display: block;
  position: absolute;
  width: 34px;
  height: 4px;
  bottom: 0;
  left: 50%;
  transform: translate(-50%, 0);
}
.el-menu-item:hover {
  background: 0 !important;
}
.el-menu-item {
  background: 0 !important;
  color: #fff !important;
}

.header .el-menu--horizontal > .el-menu-item {
  padding: 0 !important;

  margin: 0 32px !important;
}
.el-menu--horizontal > .el-menu-item {
  height: 48px !important;
  line-height: 48px !important;
}
.navBarWrap {
  position: fixed;
  top: 0;
  z-index: 999;
  background: rgba(16, 31, 22, 0.89);
}
.el-menu--horizontal > .el-submenu .el-submenu__icon-arrow {
  display: none !important;
}
.el-menu--horizontal > .el-submenu.is-active .el-submenu__title {
  border: 0;
  color: #70f4a5;
  background: 0;
}
.el-submenu__title i {
  color: #70f4a5;
}
.el-menu--horizontal > .el-submenu:hover {
  background: 0 !important;
}
.is-opened {
  background: 0 !important;
}

.navs {
  width: 16%;
  float: right;
  margin-right: 10%;
}
.el-drawer.rtl {
  background: rgba(38, 53, 44, 1);
}
.navList .el-menu--horizontal > .el-menu-item {
  padding: 0;
  width: 100%;
  text-align: center;
}
.navList .el-menu--horizontal > .el-menu-item.is-active {
  border-left: 2px solid #70f4a5;
  font-size: 18px;
  border-bottom: 0;
  color: #70f4a5;
}
.navList .el-menu--horizontal > .el-menu-item {
  line-height: 20px;
  height: 20px;
  margin-top: 20px;
}
.box {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  margin-right: 30px;
  text-align: right;
}
.navimg .luange {
  width: 24px;
  margin: 0 12px;
}
.navimg div {
  display: inline-block;
}
.navimg .package {
  width: 80px;
  margin: 0 12px;
}
.box .item img {
  width: 24px;
  margin: 0 12px;
}
.navimgList {
  text-align: center;
  margin: 30px 0 50px;
}
.navimgList .luange {
  width: 24px;
  margin-right: 20px;
}
.navimgList .package {
  width: 80px;
}
.itemList {
  position: absolute;
  bottom: 40px;
  width: 80%;
  left: 50%;
  transform: translate(-50%, 0);
  display: flex;
  justify-content: space-evenly;
}
.itemList img {
  width: 24px;
}
.el-dialog {
  background: rgba(38, 53, 44, 1);
  border-radius: 16px;
  overflow: hidden;
}
.el-dialog__header {
  display: none;
}
.el-dropdown-menu {
  border: 0;
  background: rgba(112, 244, 165, 1) !important;
}
.el-popper[x-placement^="bottom"] .popper__arrow::after {
  border-bottom-color: rgba(112, 244, 165, 1) !important;
}
.el-dropdown-menu__item {
  color: rgba(19, 29, 23, 0.8);
}
ul li {
  font-style: normal;
  list-style: none;
}
p,
li,
ul {
  margin: 0;
  padding: 0;
}
.pcmain .el-dialog--center .el-dialog__body {
  background: rgba(38, 53, 44, 1) !important;
  padding: 20px;
}
.main .el-dialog--center .el-dialog__body {
  background: rgba(38, 53, 44, 1) !important;
  padding: 10px;
}
</style>
