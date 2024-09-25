<template>
  <div class="app-wrapper">

    <sidebar :style="{ width: isOpened ? '180px' : '54px' }" :isOpened='isOpened' />
    <div class="main-container" :style="{ width: isOpened ? 'calc(100% - 180px)' : 'calc(100% - 54px)' }">
      <div class=" fixed-header">
        <navbar @open="open" />
        <tag-views />

      </div>
      <app-main />
    </div>

  </div>
</template>

<script>
import { Navbar, Sidebar, TagViews, AppMain, } from './components';
// import ResizeMixin from './mixin/ResizeHandler';

export default {
  name: 'Layout',
  components: {
    Navbar,
    Sidebar,
    TagViews,
    AppMain,
  },
  data() {
    return {
      isOpened: false
    }
  },
  methods: {

    open(val) {
      this.isOpened = val
    }
  },
};
</script>

<style lang="scss" scoped>
@import '~@/styles/mixin.scss';

.app-wrapper {
  @include clearfix;
  position: relative;
  height: 100%;
  width: 100%;
  display: flex;

  :deep(.sidebar-container) {
    transition: width 0.28s;
    width: 180px;
    background-color: #304156;
    height: 100%;
    overflow: hidden;

    .horizontal-collapse-transition {
      transition: 0s width ease-in-out, 0s padding-left ease-in-out, 0s padding-right ease-in-out;
    }

    .scrollbar-wrapper {
      overflow-x: hidden !important;
    }

    .el-scrollbar {
      height: 100%;
    }

    .el-menu {
      border: none;
      height: 100%;
      width: 100% !important;

      .el-menu-item {
        text-align: left;
      }
    }
  }

  .main-container {
    flex: 1;
    position: relative;

    .fixed-header {
      position: absolute;
      top: 0;
      right: 0;
      z-index: 9;
      width: 100%;
      transition: width 0.28s;
    }
  }
}
</style>
