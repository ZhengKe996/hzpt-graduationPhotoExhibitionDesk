<template>
  <div class="welcome">
    <div class="content">
      <div class="sub-title">欢迎使用</div>
      <div class="title">杭州科技职业技术学院毕业照片留念</div>
      <div class="desc">— 杭州科技职业技术学院&nbsp;&nbsp;物联网技术学院</div>
    </div>
    <div class="img"></div>
  </div>
</template>

<script setup></script>

<style lang="scss" scoped>
.welcome {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  background-color: #fff;
  margin-top: 6%;
  .content {
    position: relative;
    bottom: 40px;
    .sub-title {
      font-size: 30px;
      line-height: 42px;
      color: #333;
    }
    .title {
      font-size: 40px;
      line-height: 62px;
      color: #409eff;
    }
    .desc {
      text-align: right;
      font-size: 14px;
      color: #999;
    }
  }
  .img {
    margin-left: 105px;
    background-image: url("@/assets/images/welcome.png");
    width: 371px;
    height: 438px;
  }
}
</style>
