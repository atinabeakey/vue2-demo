<template>
    <div class="pie-chart"></div>
</template>
<script>
import * as echarts from "echarts";
import { debounce } from "lodash";
let myChart = null
export default {
    data() {
        return {

        }
    },
    methods: {
        initChart() {
            myChart = echarts.init(document.querySelector('.pie-chart'))
            const data = 40
            const option = {
                tooltip: { formatter: '{a}  : {c}' },
                series: [
                    //底层圆
                    {
                        type: 'gauge',
                        name: '实时功率',
                        radius: '85%', // 位置
                        center: ['50%', '50%'],
                        startAngle: 225,
                        endAngle: -45,

                        axisLine: {
                            show: true,
                            roundCap: true,
                            lineStyle: {
                                // 轴线样式
                                width: 10, // 宽度
                                color: [[1, '#e6edf0']] // 颜色
                            }
                        },
                        detail: {
                            // 仪表盘详情
                            show: false
                        },
                        pointer: {
                            icon: 'path://M2,0 L2.5,0 L3,100 L1.5,100z',
                            length: '20%',
                            offsetCenter: [0, '-45%'],
                            itemStyle: {
                                color: '#04d9c3'
                            }
                        },
                        axisTick: {
                            // 刻度
                            show: false
                        },
                        splitLine: {
                            lineStyle: {
                                color: 'auto',
                            },
                            distance: 0,
                        },
                        axisLabel: {
                            show: true,
                            // distance: 20,
                            color: '#999'
                        },
                        title: {
                            offsetCenter: [0, '-10%'],
                            fontSize: 20
                        },

                        data: [
                            {
                                value: data,

                            }
                        ]
                    },
                    //有色圆
                    {
                        type: 'gauge',
                        radius: '89%', // 位置
                        center: ['50%', '50%'],
                        zlevel: 2,
                        startAngle: 225,
                        endAngle: -45,
                        axisLine: {
                            show: true,
                            // roundCap: true,
                            lineStyle: {
                                // 轴线样式
                                width: 20, // 宽度
                                color: [
                                    [
                                        data / 100,
                                        {
                                            type: 'linear',
                                            x: 0,
                                            y: 1,
                                            x2: 0,
                                            y2: 0,
                                            colorStops: [
                                                {
                                                    offset: 0,
                                                    color: 'rgba(4,217,195,0)' // 0% 处的颜色
                                                },
                                                {
                                                    offset: 0.5,
                                                    color: 'rgba(4,217,195,0.5)' // 100% 处的颜色
                                                },
                                                {
                                                    offset: 1,
                                                    color: 'rgba(4,217,195,0.9)' // 100% 处的颜色
                                                }
                                            ],
                                            global: false // 缺省为 false
                                        }
                                    ]
                                ] // 颜色
                            }
                        },
                        axisTick: {
                            // 刻度
                            show: false
                        },
                        splitLine: {
                            // 分割线
                            show: false
                        },
                        axisLabel: {
                            // 刻度标签
                            show: false
                        },
                        pointer: {
                            icon: 'path://M12.8,0.7l12,40.1H0.7L12.8,0.7z',
                            length: '12%',
                            width: 20,
                            offsetCenter: [0, '-60%'],
                            itemStyle: {
                                color: 'auto'
                            }
                        },
                        detail: {
                            // 仪表盘详情
                            show: false
                        }
                    },

                    {
                        name: '实时功率',
                        tooltip: {
                            show: true
                        },
                        type: 'pie',
                        radius: ['0%', '40%'],
                        center: ['50%', '50%'],
                        hoverAnimation: false,
                        itemStyle: {
                            normal: {
                                color: '#fff',
                                shadowBlur: 50,
                                shadowOffsetX: 0,
                                shadowColor: 'rgba(2, 2, 2, 0.1)'
                            },
                            emphasis: {
                                color: '#fff'
                            }
                        },
                        label: {
                            normal: {
                                show: true,
                                position: 'center',
                                formatter: function (params) {
                                    return (
                                        '{value|' +
                                        params.value +
                                        '}\n{name|' +
                                        params.name +
                                        '}\n{name|kW·h}'
                                    );
                                },
                                rich: {
                                    value: {
                                        fontSize: 24,
                                        color: '#182c2f',
                                        verticalAlign: 'bottom'
                                    },
                                    name: {
                                        fontSize: 14,
                                        color: '#a7b1b7',
                                        lineHeight: 23
                                    }
                                }
                            }
                        },
                        labelLine: {
                            normal: {
                                show: false
                            }
                        },
                        animation: false,
                        data: [{ value: data, name: '实时功率' }]
                    }
                ]
            };

            myChart.setOption(option)
            window.addEventListener('resize', () => {
                myChart.resize()
            })

        },
        //监听页面变化
        resizeObserver() {
            const resizeObserver = new ResizeObserver(entries => {
                debounce(() => {
                    myChart.resize()
                }, 500)

            })
            const node = document.querySelector('.main-container')
            resizeObserver.observe(node)

        }
    },
    mounted() {
        this.initChart()

        this.resizeObserver()


    }
}
</script>
<style lang="scss" scoped>
.pie-chart {
    height: 400px;
}
</style>