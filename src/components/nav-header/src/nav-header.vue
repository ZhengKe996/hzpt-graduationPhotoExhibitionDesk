<template>
  <div class="nav">
    <el-row class="nav-item">
      <el-col :span="10" class="item-img">
        <img src="~@/assets/images/logo.png" />
      </el-col>
      <el-col :span="14">
        <img src="~@/assets/images/header-bg.png" />
      </el-col>
    </el-row>
  </div>
</template>

<style lang="scss" scoped>
.nav {
  width: 100%;
  height: 128px;
  background-color: #0068b7;
  .nav-item {
    width: 1000px;
    height: 100%;
    margin: 0 auto;
    .item-img {
      padding-top: 26px;
    }
  }
}
</style>
