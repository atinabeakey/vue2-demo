<template>
  <section class="app-main">
    <transition name="fade-transform" mode="out-in">
      <el-scrollbar class="app-scrollwrapper" wrap-class="hidden-x">
        <router-view :key="key" />
      </el-scrollbar>
    </transition>
  </section>
</template>

<script>
export default {
  name: 'AppMain',
  computed: {
    key() {
      return this.$route.path
    }
  }
}
</script>

<style lang="scss" scoped>
.app-main {
  // height: calc(100vh - 50px);
  height: 100%;
  width: 100%;
  position: relative;
  overflow: hidden;

  .app-scrollwrapper {
    height: 100%;
    overflow-x: hidden !important;

    :deep(.hidden-x) {
      overflow-x: hidden !important;
    }
  }
}

.fixed-header+.app-main {
  padding-top: 90px;
}
</style>
