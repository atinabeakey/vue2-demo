<template>
    <div class="line-charts"></div>
</template>

<script>
import * as echarts from "echarts";
import { debounce } from "lodash";
let myChart = null
export default {
    props: ['timeKey'],
    data() {
        return {
            chartData: {
                1: {
                    xAxis: ['00:00', '00:15', '00:30', '00:45', '01:00', '01:15'],
                    gl: [20, 34, 45, 67, 45, 98],
                    dl: [240, 84, 99, 56, 235, 68]
                },
                2: {
                    xAxis: ['07-01', '07-02', '07-03', '07-04', '07-06', '07-08'],
                    gl: [120, 34, 45, 67, 24, 98],
                    dl: [40, 84, 99, 56, 115, 68]
                },
                3: {
                    xAxis: ['1月', '2月', '3月', '4月', '5月', '6月'],
                    gl: [20, 34, 45, 67, 245, 98],
                    dl: [240, 84, 99, 56, 215, 68]


                },
                4: {
                    xAxis: ['2011', '2013', '2014', '2015', '2018', '2019'],
                    gl: [120, 34, 45, 67, 245, 98],
                    dl: [40, 84, 99, 56, 215, 68]
                }
            }
        }
    },
    watch: {
        timeKey(val) {
            console.log(val, '-9eeee')
            this.initChart()
        }
    },
    methods: {
        initChart() {
            if (myChart != null && myChart.dispose) {
                myChart.dispose()
            }
            myChart = echarts.init(document.querySelector('.line-charts'))
            const data = this.chartData[this.timeKey]
            const option = {
                color: ['#00d8c3', '#26a7ff'],
                toolbox: {
                    feature: {
                        // dataView: { show: true, readOnly: false },
                        // magicType: { show: true, type: ['line', 'bar'] },
                        // restore: { show: true },
                        saveAsImage: { show: true }
                    }
                },
                tooltip: {
                    trigger: 'axis'
                },
                legend: {
                    data: ['功率', '发电量'],
                    itemWidth: 10,
                    itemHeight: 3,
                    icon: 'roundRect',
                },
                xAxis: {
                    type: 'category',
                    splitLine: {
                        show: true
                    },
                    boundaryGap: false,
                    data: data.xAxis
                },
                yAxis: [
                    {
                        type: 'value',
                        name: 'KW',
                        min: 0,
                        max: 250,
                        interval: 50,

                        splitLine: {
                            show: false
                        }
                    },
                    {
                        type: 'value',
                        name: 'KWh',
                        splitLine: {
                            show: false
                        }
                    }
                ],
                series: [
                    {
                        name: '功率',
                        type: 'line',
                        tooltip: {
                            valueFormatter: function (value) {
                                return value + ' kw';
                            }
                        },
                        showSymbol: false,
                        data: data.gl
                    },
                    {
                        name: '发电量',
                        type: 'line',
                        yAxisIndex: 1,
                        showSymbol: false,
                        tooltip: {
                            valueFormatter: function (value) {
                                return value + ' kwh';
                            }
                        },
                        data: data.dl
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
.line-charts {
    height: 400px;
}
</style>