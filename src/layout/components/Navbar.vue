<template>
  <div class="navbar">

    <hamburger :is-active="opened" class="hamburger-container" @toggleClick="toggleSideBar" />

    <breadcrumb class="breadcrumb-container" />

    <div class="right-menu">

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
import Hamburger from '@/components/Hamburger';

export default {
  components: {
    Breadcrumb,
    Hamburger,
  },
  data() {
    return {
      opened: true
    }
  },
  methods: {
    toggleSideBar() {
      this.opened = !this.opened
      this.$emit('open', this.opened)
    },
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

  .hamburger-container {
    line-height: 46px;
    height: 100%;
    float: left;
    cursor: pointer;
    transition: background 0.3s;
    -webkit-tap-highlight-color: transparent;

    &:hover {
      background: rgba(0, 0, 0, 0.025);
    }
  }

  .breadcrumb-container {
    float: left;
  }

  .right-menu {
    float: right;
    margin-right: 20px;
    line-height: 50px;
    height: 100%;
    margin-top: 5px;

    :deep(.el-dropdown) {
      height: 100%;
    }
  }
}
</style>
