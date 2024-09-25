<template>
  <div class="navbar">

    <!-- <breadcrumb class="breadcrumb-container" /> -->
    <el-dropdown>
      <h4 class="el-dropdown-link">
        光伏 &nbsp;<i class="el-icon-caret-bottom"></i>
      </h4>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item>光伏1</el-dropdown-item>
        <el-dropdown-item>光伏1</el-dropdown-item>
        <el-dropdown-item>光伏1</el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>

    <div class="right-menu">
      <i class="el-icon-search"></i>
      <el-badge is-dot class="item">
        <i class="el-icon-bell"></i>
      </el-badge>
      <i class="el-icon-setting"></i>
      <el-dropdown @command="handleCommand">
        <el-avatar icon="el-icon-user-solid"></el-avatar>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item>个人信息</el-dropdown-item>
          <el-dropdown-item>退出登录</el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>

    </div>
  </div>
</template>

<script>
import Breadcrumb from '@/components/Breadcrumb';


export default {
  components: {
    Breadcrumb,

  },

  methods: {

    handleCommand() {
      this.$message('该功能正在开发中');
    }
  },
};
</script>

<style lang="scss" scoped>
.navbar {
  height: 50px;
  overflow: hidden;
  position: relative;
  background: #fff;
  box-shadow: 0 1px 4px rgba(0, 21, 41, 0.08);
  display: flex;
  justify-content: space-between;
  align-items: center;

  .el-dropdown-link {
    padding-left: 20px;
    cursor: pointer;
  }


  .right-menu {
    margin-right: 20px;

    display: flex;
    align-items: center;

    i {
      margin-right: 10px;
      cursor: pointer;
    }

    .item {

      // margin-top: 10px;
      :deep(.el-badge__content.is-fixed.is-dot) {
        right: 17px;
        top: 5px;
      }
    }

    :deep(.el-dropdown) {
      height: 100%;
    }
  }
}
</style>
