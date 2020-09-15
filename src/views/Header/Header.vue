<template>
  <header>
    <div class="top-bar">
      <div class="bar-container">
        <div class="nav-container">
          <ul class="nav">
            <li class="nav-item" v-for="(item, index) in navsData" :key="index">
              <div class="item-style" v-if="item.value === '小米商城'">
                <a :href="item.url">{{ item.value }}</a>
              </div>
              <div class="item-style" v-if="item.value !== '小米商城'">
                <a :href="item.url" target="_blank">{{item.value}}</a>
              </div>
              <span class="nav-span" v-show="index !== navsData.length - 1">|</span>
            </li>
          </ul>
        </div>
        <div class="nav-login">
          <ul class="nav-login-item">
            <li class="nav-item" v-for="(item,index) in loginData" :key="index">
              <a :href="item.url" target="_blank">{{item.value}}</a>
              <span class="nav-span" v-show="index !== loginData.length - 1">|</span>
            </li>
          </ul>
          <div class="nav-cart" @mouseenter="cartListShow" @mouseleave="cartListHide">
            <div class="nav-cart-container" :class="{'active': showFlag}">
              <i class="iconfont icon-cart"></i>
              <a href="http://static.mi.com/cart/">
                购物车(
                <span>0</span>
                )
              </a>
            </div>
            <transition name="fade-in">
              <div class="nav-cart-list" v-show="showFlag">
                <div class="cart-list-word">购物车中还没有商品，赶快选购吧！</div>
              </div>
            </transition>
          </div>
        </div>
      </div>
    </div>
    <div class="top-header">
      <div class="top-container">
        <a class="mi-icon" href="#"></a>
        <div class="header-navs-container">
          <div class="divider"></div>
          <ul class="navs">
            <li class="navs-item" v-for="(item, index) in rdata.navs" :key="index">
              <a
                v-if="item.type"
                :data-type="item.type"
                @mouseenter="menusListShow(item.type)"
                @mouseleave="menusListHide()"
              >{{item.value}}</a>
              <a v-else :href="item.url" target="_blank">{{item.value}}</a>
            </li>
          </ul>
        </div>
        <div class="header-search-container">
          <input
            @focus="searchListShow"
            @blur="searchListHide"
            class="search-input"
            :class="{'active': focusFlag}"
            type="search"
            value
          />
          <label
            class="search-btn"
            :class="{'active': focusFlag}"
            style="width:52px;height:50px;border-left: 0;"
          >
            <i class="iconfont icon-search-copy"></i>
          </label>
          <ul class="search-list" v-show="!hotsListFlag">
            <li class="list-item" v-for="(item, index) in rdata.hots" :key="index">{{item}}</li>
          </ul>
        </div>
      </div>
      <transition name="menu-trans">
        <div
          class="menus-list"
          @mouseenter="menusListShow()"
          @mouseleave="menusListHide()"
          v-show="menusListFlag"
        >
          <ul class="menus">
            <li class="menus-item" v-for="(item, index) in menusItemData" :key="index">
              <a :href="item.src">
                <img class="item-img" :src="item.url" />
              </a>
              <div class="item-value">{{item.value}}</div>
              <div class="item-type" v-if="item.type">{{item.type}}</div>
              <div class="item-price" v-if="item.price && item.sub">{{item.price}}元起</div>
              <div class="item-price" v-if="item.price && !item.sub">{{item.price}}元</div>
            </li>
          </ul>
        </div>
      </transition>
    </div>
  </header>
</template>

<script>
import axios from "axios";
export default {
  created() {
    // let httpUrl = `https://easy-mock.com/mock/5f5e3fb43d4341430587980f/`;
    let httpUrl = `http://rap2.taobao.org:38080/app/mock/266491/header`;
    axios.get(httpUrl).then((res) => {
      this.rdata = res.data;
    });
  },
  data() {
    return {
      rdata: {},
      navsData: [
        { value: "小米商城", url: "https://www.mi.com/index.html" },
        { value: "MIUI", url: "https://www.miui.com/" },
        { value: "loT", url: "https://iot.mi.com/index.html" },
        { value: "云服务", url: "https://i.mi.com/" },
        { value: "金融", url: "https://jr.mi.com?from=micom" },
        { value: "有品", url: "https://youpin.mi.com/" },
        { value: "小爱开放平台", url: "https://xiaoai.mi.com/" },
        { value: "企业团购", url: "https://qiye.mi.com/" },
        { value: "资质证照", url: "https://www.mi.com/aptitude/list/?id=41" },
        { value: "协议规则", url: "https://www.mi.com/aptitude/list/" },
        { value: "下载app", url: "https://www.mi.com/appdownload/" },
        { value: "Select Location", url: "javascript:void(0);" },
      ],
      loginData: [
        {
          value: "登陆",
          url:
            "http://order.mi.com/site/login?redirectUrl=http://www.mi.com/index.html",
        },
        { value: "注册", url: "https://account.xiaomi.com/pass/register" },
        { value: "消息通知", url: "http://order.mi.com/message/list" },
      ],
      showFlag: false,
      menusListFlag: false,
      menusItemData: {},
      timer: "",
      hotsListFlag: true,
      focusFlag: false,
    };
  },
  methods: {
    cartListShow() {
      this.showFlag = true;
    },
    cartListHide() {
      this.showFlag = false;
    },
    // 菜单显示区域
    menusListShow(type) {
      if (type) {
        this.menusItemData = this.rdata[type];
      }
      this.menusListFlag = true;
      clearTimeout(this.timer);
    },
    menusListHide() {
      this.timer = setTimeout(() => {
        this.menusListFlag = false;
      }, 100);
    },
    // 搜索框下拉列表
    searchListShow() {
      this.hotsListFlag = false;
      this.focusFlag = true;
    },
    searchListHide() {
      this.hotsListFlag = true;
      this.focusFlag = false;
    },
  },
};
</script>

<style lang="less" scoped>
@import "@/assets/css/header.less";
</style>
