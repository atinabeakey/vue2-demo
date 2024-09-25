<template>
  <div class="sidebar-container">
    <el-scrollbar wrap-class="scrollbar-wrapper">
      <el-menu :default-active="activeMenu" :collapse="!isOpened" :unique-opened="false" background-color="#304156"
        text-color="#fff" active-text-color="#1ddcc9" :collapse-transition="false" mode="vertical"
        @select="handleSelect">
        <sidebar-item v-for="route in routes" :key="route.path" :item="route" />
      </el-menu>
    </el-scrollbar>
  </div>
</template>

<script>
import SidebarItem from './SidebarItem';

export default {
  components: { SidebarItem },
  props: ['isOpened'],
  computed: {
    routes() {
      return this.$router.options.routes;
    },
    activeMenu() {
      const route = this.$route;
      const { meta, path } = route;
      if (meta.activeMenu) {
        return meta.activeMenu;
      }
      return path;
    },

  },
  methods: {
    handleSelect(key, keypath) {
      this.$router.push(key)
    },
  }
};
</script>
