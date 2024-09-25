<template>
  <div class="sidebar-container">
    <el-scrollbar wrap-class="scrollbar-wrapper">
      <el-menu :default-active="activeMenu" :collapse="!opened" :unique-opened="false" background-color="#304156"
        text-color="#fff" active-text-color="#1ddcc9" :collapse-transition="false" mode="vertical"
        @select="handleSelect">
        <sidebar-item v-for="route in routes" :key="route.path" :item="route" />
      </el-menu>
    </el-scrollbar>
    <hamburger :is-active="opened" class="hamburger-container" @toggleClick="toggleSideBar" />
  </div>
</template>

<script>
import SidebarItem from './SidebarItem';
import Hamburger from '@/components/Hamburger';
export default {
  components: { SidebarItem, Hamburger },
  data() {
    return {
      opened: false
    }
  },

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
    toggleSideBar() {
      this.opened = !this.opened
      this.$emit('open', this.opened)
    },
  }
};
</script>
<style lang="scss" scoped>
.hamburger-container {
  position: fixed;
  bottom: 20px;
}
</style>
