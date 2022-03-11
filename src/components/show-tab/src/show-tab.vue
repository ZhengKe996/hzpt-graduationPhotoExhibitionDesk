<template>
  <el-menu
    class="el-menu-demo"
    mode="horizontal"
    background-color="#ffffff"
    text-color="#0c2135"
    active-text-color="#ffffff"
    :ellipsis="false"
    @select="handleMarjorClick"
  >
    <template v-for="marjor of marjorList" :key="marjor.id">
      <el-menu-item :index="marjor.id + ''">{{ marjor.marjor }}</el-menu-item>
    </template>
  </el-menu>
  <banner class="banner" :infoMation="infoMation" />
</template>

<script setup>
import { defineProps, ref, reactive, onMounted } from "vue";
import Banner from "@/components/banner";
import { INFOMATION } from "@/config";
import ownRequest from "@/service";
const marjorName = ref(1);
const className = ref();
let classList = reactive([]);
const infoMation = ref([]);
const props = defineProps({
  marjorList: Array,
  collegeId: Number,
  years: String,
});
onMounted(() => {
  getClass(marjorName.value);
});

const handleMarjorClick = (key) => {
  getClass(key);
  marjorName.value = key;
};

const handleClassClick = () => {
  ownRequest.get({ url: `/${INFOMATION}/${className.value}` }).then((res) => {
    const { data } = res.data;
    infoMation.img = JSON.parse(data.img);
    infoMation.cnaeme = data.cname;
  });
};

const getClass = (mid) => {
  infoMation.value = infoMation.value.slice(0, 0);
  classList.length = 0;
  ownRequest
    .get({
      url: `/${INFOMATION}/findClass?cid=${props.collegeId}&mid=${mid}&years=${props.years}`,
    })
    .then((res) => {
      const { data } = res.data;
      classList.push(...data);
      classList.forEach((item) => {
        getInfo(item.id);
      });
    });
};
const getInfo = (id) => {
  ownRequest.get({ url: `/${INFOMATION}/${id}` }).then((res) => {
    const { data } = res.data;
    data.img = JSON.parse(data.img);
    if (data.img.length > 0) {
      infoMation.value.push(...data.img);
    }
  });
};
</script>

<style lang="scss" scoped>
.el-menu {
  border-right: none;
}
.el-sub-menu {
  background-color: #ffffff !important;

  // 二级菜单 ( 默认背景 )
  .el-menu-item {
    /* padding-left: 50px !important; */
    background-color: #ffffff !important;
  }
}

::v-deep .el-sub-menu__title {
  background-color: #ffffff !important;
  margin: 0 !important;
}

// hover 高亮
.el-menu-item:hover {
  color: #fff !important; // 菜单
  background-color: #075aa6 !important;
}

.el-menu-item.is-active {
  color: #fff !important;
  background-color: #075aa6 !important;
}

.banner {
  margin-top: 10px;
}
</style>
