<template>
  <div class="nav-menu">
    <el-menu
      background-color="#ffffff"
      text-color="#0c2135"
      active-text-color="#ffffff"
      :unique-opened="true"
      menu-trigger="hover"
      @select="handleSelect"
    >
      <template v-for="college of props.collegeList" :key="college.id">
        <el-sub-menu :index="JSON.stringify({ college: college.id })">
          <template #title>
            <span>{{ college.college }}</span>
          </template>
          <el-menu-item-group title="毕业年份">
            <template v-for="year of college.years" :key="year">
              <el-menu-item
                :index="JSON.stringify({ college: college.id, year: year })"
              >
                {{ year }}年
              </el-menu-item>
            </template>
          </el-menu-item-group>
        </el-sub-menu>
      </template>
    </el-menu>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

const props = defineProps({
  collegeList: Array,
  yearList: Array,
});

const emit = defineEmits(["getYears", "getMarjor", "getClass"]);

const handleClass = (cid, year) => {
  emit("getMarjor", cid, year);
};

const handleSelect = (key) => {
  const query = JSON.parse(key);
  handleClass(query.college, query.year);
};
</script>

<style lang="scss" scoped>
.nav-menu {
  height: 100%;
  background-color: #ffffff;

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
}
</style>
