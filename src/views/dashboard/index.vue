<template>

  <div class="dashboard-container">
    <el-scrollbar wrap-class="scrollbar-wrapper">
      <el-container>
        <el-header>Header</el-header>
        <el-container class="dashboard-main">
          <el-aside width="320px">
            <div class="tree-list">
              <el-input placeholder="请输入搜索内容" v-model="filterText" suffix-icon="el-icon-search" size="small" />
              <el-tree class="filter-tree" :data="data" :props="defaultProps" default-expand-all
                :filter-node-method="filterNode" ref="tree">
              </el-tree>
            </div>
          </el-aside>
          <el-main>
            <div class="content">
              <el-container class="dashboard-main">
                <el-aside width="280px">
                  <basic-info class="common-border" />
                </el-aside>
                <el-main>

                  <div class="common-border">
                    <pie-chart />
                    <line-chart />
                  </div>

                  <table-list class="common-border" />
                </el-main>
              </el-container>
            </div>
          </el-main>
        </el-container>
      </el-container>
    </el-scrollbar>
  </div>
</template>

<script>
import BasicInfo from './components/BasicInfo.vue';
import TableList from './components/table.vue';
import PieChart from './components/PieChart.vue';
import LineChart from './components/LineChart.vue';
export default {
  name: 'Dashboard',
  components: { BasicInfo, TableList, PieChart, LineChart },
  data() {
    return {
      filterText: '',
      data: [{
        id: 1,
        label: '良信海盐光伏站',
        children: [{
          id: 2,
          label: '光伏逆变器 1-1'
        },
        {
          id: 3,
          label: '光伏逆变器 1-2'
        }, {
          id: 4,
          label: '光伏逆变器 1-3'
        }, {
          id: 5,
          label: '光伏逆变器 1-4'
        }]
      }],
      defaultProps: {
        children: 'children',
        label: 'label'
      }
    };
  },
  watch: {
    filterText(val) {
      this.$refs.tree.filter(val);
    }
  },

  methods: {
    filterNode(value, data) {
      if (!value) return true;
      return data.label.indexOf(value) !== -1;
    }
  },
};
</script>

<style lang="scss" scoped>
.dashboard-container {
  background: #F2F4F5;

  .common-border {
    border: 2px solid #f2f2f2;
    border-radius: 6px;
  }

  .dashboard-main {
    margin: 0 15px 15px;
    @extend .common-border;
    background: #fff;

    .tree-list {
      padding: 20px;
      height: 100%;
      border-right: 2px solid #f2f2f2;

      // width: 300px;
      .filter-tree {
        margin-top: 15px;

        :deep(.el-tree-node__content) {
          height: 30px;
        }

      }
    }


  }

}
</style>
