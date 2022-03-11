<template>
  <div class="basic-layout">
    <nav-header />
    <div class="nav-side">
      <nav-menu
        :collegeList="collegeList"
        :yearList="yearList"
        @getMarjor="getMarjor"
      />
    </div>
    <div class="content-right">
      <div class="wrapper">
        <div class="main-page">
          <el-row>
            <el-col :span="24">
              <show-tab
                v-if="showWelcome"
                :collegeId="collegeId"
                :years="years"
                :marjorList="marjorList"
              />
              <welcome v-else />
            </el-col>
          </el-row>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, reactive } from "vue";
import NavHeader from "@/components/nav-header";
import NavMenu from "@/components/nav-menu";
import ShowTab from "@/components/show-tab";
import Welcome from "@/views/welcome";

import ownRequest from "@/service";
import { INFOMATION } from "@/config";
const showWelcome = ref(false);
const collegeId = ref();
const years = ref();
const collegeList = ref([]);
const yearList = ref([]);
const marjorList = ref([]);

onMounted(() => {
  getCollege();
});

const getCollege = () => {
  ownRequest.get({ url: `${INFOMATION}/findAllCidYears` }).then((res) => {
    const { data: list } = res.data;
    collegeList.value = list;
  });
};

const getMarjor = (cid, year) => {
  showWelcome.value = true;
  collegeId.value = cid;
  years.value = year;
  ownRequest
    .get({ url: `/${INFOMATION}/findMarjor?cid=${cid}&years=${year}` })
    .then((res) => {
      const { data } = res.data;
      marjorList.value = data;
    });
};
</script>

<style lang="scss" scoped>
.basic-layout {
  position: relative;
  height: 100vh;
  width: 100vw;
  background-image: url("@/assets/images/login-bg.svg");

  .nav-side {
    position: fixed;
    width: 210px;
    height: 100vh;
    background-color: #0c2135;
    color: #fff;
    overflow-y: auto;
    transition: width 0.5s;
  }
  .content-right {
    margin-left: 210px;

    .wrapper {
      background: #eef0f3;

      padding: 20px;
      height: calc(100vh - 128px);
      .main-page {
        background-color: #fff;
        background-image: url("@/assets/images/login-bg.svg");
        height: 100%;
        padding: 40px;
      }
    }
  }
}
</style>
