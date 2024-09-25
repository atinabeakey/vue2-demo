<template>
    <div>
        <div class="table-header">
            <h4>运行参数</h4>
            <div class="table-right">
                <p>数据更新时间：2023/05/29 16:58:20</p>
                <ul>
                    <li v-for="item in tabList" :key="item.key" :class="{ active: activeName === item.key }"
                        @click="handleClick(item)">
                        {{ item.label }}
                    </li>
                </ul>
            </div>

        </div>
        <div class="table-content">
            <div class="left">
                <div class="common">
                    <div class="common">
                        <p></p>
                        <b>直流输入</b>
                    </div>
                    <ul>
                        <li v-for="(item, index) in tableList" :key="index" :class="{ active: action === item.label }"
                            @click="handleTabClick(item)">
                            {{ item.label }}
                        </li>
                    </ul>
                </div>
                <el-table :data="tableData" show-summary style="width: 100%" height="300">
                    <el-table-column prop="name" label="参数"> </el-table-column>
                    <el-table-column prop="dy" label="输入电压（V）">
                    </el-table-column>
                    <el-table-column prop="dl" label="输入电流（A）">
                    </el-table-column>

                </el-table>
            </div>
            <div class="right">
                <div class="common">
                    <div class="common">
                        <p></p>
                        <b>交流输出</b>
                    </div>
                </div>
                <el-table :data="tabRightData" show-summary style="width: 100%" height="300">
                    <el-table-column prop="name" label="参数" width="150"> </el-table-column>
                    <el-table-column prop="a" label="A相">
                    </el-table-column>
                    <el-table-column prop="b" label="B相">
                    </el-table-column>
                    <el-table-column prop="c" label="C相">
                    </el-table-column>
                </el-table>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            tabList: [
                { label: "实时数据", key: 1 },
                { label: "历史趋势", key: 2 },
            ],
            tableList: [
                { label: "PV", },
                { label: "MPPT", },
            ],
            activeName: 1,
            action: 'PV',
            tableData: [],
            tabRightData: [
                { name: '电压（V）', a: 0, b: 0, c: 0 },
                { name: '电流（A）', a: 0, b: 0, c: 0 },
                { name: '总有功功率（kW)', a: 0, b: 0, c: 0 },
                { name: '功率因素', a: 1, b: 0, c: 0 },
                { name: '频率（HZ）', a: 1, b: 0, c: 0 },
            ]
        };
    },
    methods: {
        handleClick(item) {
            this.activeName = item.key
        },
        //生成数据
        setData() {
            this.tableData = new Array(5).fill(1).map((item, index) => {
                return {
                    name: `${this.action}${index + 1}`,
                    id: index + 1,
                    dy: Math.floor(Math.random() * 100) + 1,
                    dl: Math.floor(Math.random() * 100) + 1
                }
            })
        },
        handleTabClick(item) {
            this.action = item.label
            this.setData()
        }
    },
    created() {
        this.setData()
    }
};
</script>
<style lang="scss">
.common {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.table-header {
    @extend .common;
    padding-bottom: 20px;

    .table-right {
        @extend .common;

        p {
            font-size: 12px;
            color: #ccc
        }
    }

    ul {
        display: flex;
        margin-left: 10px;

        li {
            padding: 5px 10px;

            cursor: pointer;
            display: flex;
            align-items: center;
            position: relative;
            border: 1px solid #f2f2f2;
            font-size: 14px;
            border-radius: 6px;
            color: #9aa1a7;

            &:nth-of-type(1) {
                border-top-right-radius: 0;
                border-bottom-right-radius: 0;
            }

            &:nth-of-type(2) {
                border-top-left-radius: 0;
                border-bottom-left-radius: 0;
            }

            &.active {
                border-color: #939598;
                color: #939598
            }
        }
    }


}

.table-content {
    display: flex;

    p {
        width: 32px;
        height: 32px;
        margin-right: 5px;
    }

    .left {
        width: 50%;
        padding-right: 20px;
        border-right: 1px solid #f2f2f2;

        p {
            background: url('@/assets/img/import.png') no-repeat;
            background-size: 100% 100%;

        }

        ul {
            display: flex;
            align-items: center;
            width: 100px;
            height: 30px;
            background: #f2f3f4;
            border-radius: 2px;
            padding: 3px;

            li {
                width: 47px;
                font-size: 14px;
                height: 100%;
                line-height: 24px;
                text-align: center;
                border-radius: 2px;
                cursor: pointer;

                &.active {
                    background: #fff;
                }

            }
        }
    }

    .right {
        width: 50%;
        padding-left: 20px;
        // flex: 1;

        p {
            background: url('@/assets/img/export.png') no-repeat;
            background-size: 100% 100%;

        }
    }


}
</style>