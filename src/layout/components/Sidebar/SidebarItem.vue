<template>
  <div v-if="!item.hidden">
    <template v-if="
      hasOneShowingChild(item.children, item) &&
      (!onlyOneChild.children || onlyOneChild.noShowingChildren) &&
      !item.alwaysShow
    ">
      <el-menu-item :index="onlyOneChild.path">
        <svg-icon :icon="onlyOneChild.meta.icon || (item.meta && item.meta.icon)" />
        <span slot="title">{{ onlyOneChild.meta.title }}</span>
      </el-menu-item>
    </template>

    <el-submenu v-else ref="subMenu" :index="item.path" popper-append-to-body>
      <template slot="title">
        <svg-icon v-if="item.meta" :icon="item.meta && item.meta.icon" :title="item.meta.title" />
        <span slot="title">{{ item.meta.title }}</span>

      </template>
      <sidebar-item v-for="child in item.children" :key="child.path" :is-nest="true" :item="child" class="nest-menu" />
    </el-submenu>
  </div>
</template>

<script>
import SvgIcon from './Icon';

export default {
  name: 'SidebarItem',
  components: { SvgIcon, },
  props: {
    // route object
    item: {
      type: Object,
      required: true,
    },


  },
  data() {
    // TODO: refactor with render function
    this.onlyOneChild = null;
    return {};
  },
  methods: {
    hasOneShowingChild(children = [], parent) {
      const showingChildren = children.filter((item) => {
        if (item.hidden) {
          return false;
        } else {
          // Temp set(will be used if only has one showing child)
          this.onlyOneChild = item;
          return true;
        }
      });

      // When there is only one child router, the child router is displayed by default
      if (showingChildren.length === 1) {
        return true;
      }

      // Show parent if there are no child router to display
      if (showingChildren.length === 0) {
        this.onlyOneChild = { ...parent, path: '', noShowingChildren: true };
        return true;
      }

      return false;
    },

  },
};
</script>
