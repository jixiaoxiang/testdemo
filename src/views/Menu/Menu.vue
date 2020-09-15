<template>
  <div class="menu-banner">
    <div class="menu-container" @mouseleave="bannerMenuHide()">
      <ul class="menu-list">
        <li
          class="list-item"
          v-for="(item,index) in rdata.menus"
          :key="index"
          @mouseenter="bannerMenuShow(item.type)"
        >
          <a :href="item.url" target="blank">{{item.value}}</a>
          <i class="iconfont icon-arrow-right"></i>
        </li>
      </ul>
    </div>
    <div
      class="menu-info"
      v-show="bannerMenuFlag"
      @mouseleave="bannerMenuHide()"
      @mouseenter="bannerMenuShow()"
    >
      <ul class="menu-info-list" v-for="(list, key) in menuListMatch" :key="key" :data-key="key">
        <li class="info-list-item" v-for="(item, index) in list" :key="index" :data-index="index">
          <a :href="item.url">
            <img :src="item.src" :alt="item.name" />
            <span class>{{item.name}}</span>
          </a>
        </li>
      </ul>
    </div>
    <Banner :banners="banners"></Banner>
  </div>
</template>


<script>
import Banner from "../../components/Banner";
import axios from "axios";
export default {
  created() {
    let httpUrl = `http://rap2.taobao.org:38080/app/mock/266491/menu`;
    axios.get(httpUrl).then((res) => {
      console.log(res);
      this.rdata = res.data;
    });
  },
  data() {
    return {
      rdata: {},
      bannerMenuFlag: false,
      menuTimer: "",
      listInfoData: [],
      banners: [
        {
          src:
            "https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/cefed8336bae62768afeeb6a3b8f55c8.jpg?w=2452&h=920",
          url: "https://www.mi.com/redminote7/",
        },
        {
          src:
            "https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/743e04f29f920648b9d99b04a85ce343.jpg?w=2452&h=920",
          url: "https://www.mi.com/a/h/11251.html",
        },
        {
          src:
            "https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/3d7d3f2df881cf62e5fafdada94f5018.jpg?w=2452&h=920",
          url: "https://www.mi.com/mitvall-screen/e55c/",
        },
        {
          src:
            "https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/6bd4174b8c5aad67a64864a5716ad152.jpg?w=2452&h=920",
          url: "https://www.mi.com/washer-dryer-10/",
        },
        {
          src:
            "https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/a1f0eb196c6c65a89ffba6efa4b5679c.jpg?w=2452&h=920",
          url: "https://www.mi.com/a/h/11117.html",
        },
      ],
    };
  },
  methods: {
    bannerMenuHide() {
      console.log("456");
      this.menuTimer = setTimeout(() => {
        this.bannerMenuFlag = false;
      }, 100);
    },
    bannerMenuShow(type) {
      console.log("123");
      if (type) {
        this.listInfoData = this.rdata[type];
      }
      this.bannerMenuFlag = true;
      clearTimeout(this.menuTimer);
    },
  },
  computed: {
    menuListMatch() {
      if (this.listInfoData && this.listInfoData.length) {
        const matchData = [];
        for (let i = 0; i < this.listInfoData.length; i += 6) {
          matchData.push(this.listInfoData.slice(i, i + 6));
        }
        return matchData;
      }
    },
  },
  components: {
    Banner,
  },
};
</script>

<style lang="less" scoped>
@import "@/assets/css/menu.less";
</style>