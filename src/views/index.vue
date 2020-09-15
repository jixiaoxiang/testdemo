<template>
  <div class="index-page">
    <Header />
    <Menu />
    <MenuFooter />
    <div class="gray-page">
      <FlashSale />
      <Goods />
      <VideoBox />
    </div>
    <site-footer></site-footer>
    <div class="gray-page">
      <site-info></site-info>
    </div>
    <ToolBar />
    <VideoWindow />
  </div>
</template>

<script>
import Header from "./Header/Header";
import Menu from "./Menu/Menu";
import MenuFooter from "./Menu/MenuFooter";
import FlashSale from "./Article/FlashSale";
import Goods from "./Article/Goods";
import VideoBox from "./Article/VideoBox";
import VideoWindow from "../components/VideoWindow";
import SiteFooter from "./Footer/SiteFooter";
import SiteInfo from "./Footer/SiteInfo";
import ToolBar from "./Aside/ToolBar";

export default {
  components: {
    Header,
    Menu,
    MenuFooter,
    FlashSale,
    Goods,
    SiteFooter,
    SiteInfo,
    VideoBox,
    VideoWindow,
    ToolBar,
  },
};
</script>

<style lang="less" scoped>
.index-page {
  .gray-page {
    display: flex;
    flex-direction: column;
    width: 100%;
    height: auto;
    background-color: #f5f5f5;
  }
}
</style>