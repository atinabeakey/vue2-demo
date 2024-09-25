<template>

  <div class="dashboard-container">
    <el-scrollbar wrap-class="scrollbar-wrapper">
      <el-container>
        <el-header>
          <p @click="backHistory()">
            <i class="el-icon-arrow-left"></i>
            <span>{{ title }}</span>
          </p>
          <ul>
            <li v-for="item in ulList" :key="item.key" :class="{ active: actionIndex === item.key }"
              @click="toggleClick(item)">{{ item.label }}
            </li>
          </ul>
        </el-header>
        <el-container class="dashboard-main">
          <el-aside width="320px">
            <div class="tree-list">
              <el-input placeholder="请输入搜索内容" v-model="filterText" suffix-icon="el-icon-search" size="small"
                clearable />
              <el-tree class="filter-tree" node-key="id" :data="data" :props="defaultProps" default-expand-all
                :current-node-key="currentId" :filter-node-method="filterNode" ref="tree" :highlight-current="true"
                @current-change="changeTree">
              </el-tree>

            </div>
          </el-aside>
          <el-main class="content">
            <div class='content-header'>
              <h4>{{ currentNode.label }}</h4>
              <ul>
                <li v-for="item in tabList" :key="item.key" :class="{ active: activeName === item.key }"
                  @click="handleClick(item)">
                  {{ item.label }}</li>
              </ul>
            </div>
            <el-container>
              <el-aside width="280px">
                <basic-info class="common-border" />
              </el-aside>
              <el-main class="right">

                <div class="common-border ">
                  <div class="time-change">
                    <h4>功率及发电量</h4>
                    <div class="time">
                      <el-radio-group v-model="timeRadio" size="small">
                        <el-radio-button v-for="item in timeList" :key="item.key" :label="item.key">{{ item.label
                          }}</el-radio-button>
                      </el-radio-group>
                      <el-date-picker v-model="dateTime" type="date" placeholder="选择日期" style="width:150px" size="small"
                        clearable>
                      </el-date-picker>
                    </div>

                  </div>
                  <div class="chart">
                    <pie-chart />
                    <line-chart :timeKey="timeRadio" />
                  </div>

                </div>

                <table-list class="common-border" style="margin-top: 20px;" />
              </el-main>
            </el-container>
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
    const list = [{
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
    }]
    return {
      filterText: '',
      data: list,
      defaultProps: {
        children: 'children',
        label: 'label'
      },
      currentId: list[0]?.id,
      currentNode: list[0],

      ulList: [
        { label: '概览', key: 1 },
        { label: '设备', key: 2 },
      ],
      actionIndex: 1,
      tabList: [
        { label: '通行', key: 1 },
        { label: '故障', key: 2 },
        { label: '告警', key: 3 },
        { label: '配置', key: 4 },
      ],
      activeName: 1,
      timeList: [{ label: '时', key: 1 },
      { label: '日', key: 2 },
      { label: '年', key: 3 },
      { label: '生命期', key: 4 },],
      timeRadio: 1,
      dateTime: null
    };
  },

  watch: {
    filterText(val) {
      this.$refs.tree.filter(val);
    },
    currentId(val) {
      this.currentNode
    }
  },
  computed: {
    title() {
      return this.$route.meta?.title
    },
  },
  methods: {
    filterNode(value, data) {
      if (!value) return true;
      return data.label.includes(value);
    },
    toggleClick(val) {
      this.actionIndex = val.key
    },
    changeTree(val) {
      this.currentNode = val
    },
    backHistory() {
      history.go(-1)
    },
    handleClick(val) {
      this.activeName = val.key
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

  :deep(.el-header) {
    height: 40px !important;
    display: flex;
    justify-content: space-between;
    align-items: center;

    p {
      cursor: pointer;

      i {
        font-weight: 500;
      }
    }

    ul {
      background: #fff;
      display: flex;
      align-items: center;
      overflow: hidden;
      height: 30px;
      line-height: 30px;
      border-radius: 30px;

      li {
        width: 80px;
        font-size: 12px;
        text-align: center;
        height: 100%;
        border-radius: 30px;
        cursor: pointer;
        border: 1px solid transparent;
        line-height: 28px;

        &.active {
          border-color: #898c8f;
        }
      }
    }
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

    .content {
      .content-header {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding-bottom: 20px;

        ul {
          display: flex;


          li {
            padding: 0 5px;
            margin-left: 10px;
            cursor: pointer;
            display: flex;
            align-items: center;
            position: relative;


            &::after {
              content: "";
              display: inline-block;
              width: 100%;
              height: 2px;
              background: transparent;
              position: absolute;
              bottom: -8px;
              left: 0;
            }

            &.active {

              &::after {
                background: #2c3e50;
              }
            }


          }
        }
      }

      .right {
        padding: 0 0 0 20px !important;

        .common-border {
          padding: 20px;

          .time-change {
            display: flex;
            justify-content: space-between;
            align-items: center;

            .el-radio-group {
              margin-right: 20px
            }
          }

          h4 {
            font-size: 16px;
          }

          .chart {
            display: flex;
            margin-top: 20px;

            .pie-chart {
              width: 45%;
            }

            .line-charts {
              width: 65%;
            }

          }
        }

        .el-table {
          margin-top: 20px;
        }
      }
    }
  }

}
</style>
